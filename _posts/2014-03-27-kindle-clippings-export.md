---
date: 2014/03/28 00:35:45
creatdate: 2014-03-27 12:51:10
layout: post
title: Kindle 笔记格式化导出（预告）
thread: 10
categories: 作品
tags: MATLAB
---

项目更新地址：[https://github.com/HereChen/KindleClippingsExport](https://github.com/HereChen/KindleClippingsExport)

Author：[HereChen](http://herechen.github.io/)  
Version：1.0 （数据可导出，文件不可导出，不可按条件导出） 
update：2014-03-27


###项目描述

本项目旨在提取 Kindle 笔记信息，并作分离，然后实现格式化导出。这里的格式化将针对 Markdown，但最终期望是实现笔记的提取以及按条件提取，并且可以自定义导出文本格式。

###使用描述

`clipExport = KindleClippingsExport(clipImportFile, clipExportFile)`

`clipExport`--导出数据  
`clipImportFile`--笔记原始文件，如 `'My Clippings.txt'`  
`clipExportFile`--笔记导出文件名，如 `'exportclip.txt'`

`RunKindleClippingsExport.m`--是一个导出demo  
`KindleClippingsExport.m`--为导出函数

###示例

	% 2014/03/27 01:01:30
	% by HereChen
	
	clear;clc
	slCharacterEncoding('GBK')
	%%
	clipFile = 'My Clippings.txt';                  % 读取文件
	clipExport = 'ClipExportWang.txt';              % 导出文件名
	varargin = {'encoding', 'UTF-8'};
	clipExport = KindleClippingsExport(clipFile,clipExport,varargin);

###KindleClippingsExport

		function varargout = KindleClippingsExport(clipImportFile,clipExportFile,varargin)
        %KINDLECLIPPINGSEXPORT
        %   The software will convert Kindle Clippings into markdown format.
        %   Language-surpport Chinese English.
        %   1 Get clippings with segment '=========='.
        %   2 Clippings none-four lines will be ignorant.
        %   3 Test Kindle PaperWhite system 5.4.2.1.
        %
        %   clipImportFile - input Kindle Clippings txt filename.
        %   clipExportFile - export Kindle Clippings txt filename.
        %   varargin
        %       'encoding' - encoding of the way open txt-file
        %                    'UTF-8' 'GBK'
        %       'filter'   - filter the clippings with condition
        %                    'author' 'bookname'
        %   varargout - exported clippings data set.(clipExport)
        %
        %   Example...
        %   clipFile = 'My Clippings.txt';
        %   clipExport = 'ClipExport.txt';
        %   varargin = {'encoding', 'UTF-8'};
        %   clipExport = KindleClippingsExport(clipFile,clipExport,varargin);
        %
        %   In case of encoding matters...
        %   check encoding: slCharacterEncoding()
        %   set encoding: slCharacterEncoding('GBK') or 'UTF-8'

        %   HereChen
        %   (chenlei.here@gmail.com)(herechen.github.io)
        %   Copyright 2014 HereChen
        %   $Date: 2014/03/28 00:35:45 $

        %% deault settings

        % default encoding of open txt-file.
        encoding = 'UTF-8';
        % default filter, no filter.
        filter = '';

        % varargin
        nVarargs = length(varargin);
        if nargin < 2, error('At least two input arguments'); end
        if nVarargs > 4, error('At most six output arguments'); end
        for k=1:2:nVarargs
            varMark = 0;
            if strcmp(varargin{k},'filter')
                filter = varargin{k+1};
                varMark = 1;
            elseif strcmp(varargin{k},'encoding')
                encoding = varargin{k+1};
                varMark = 1;
            end
            if varMark
                error('No such argument %s.',char(varargin{k}));
            end
        end

        % varargout
        if nargout == 0, varargout = {}; end
        if nargout > 1, error('At most one output arguments'); end

        % segment of clippings
        segClip = '==========';

        %% read every line of clipImportFile

        fileID = fopen(clipImportFile,'r','n',encoding);
        formatSpec = '%s';                          % 读取格式
        clippings = textscan(fileID,formatSpec,...  % 读取，忽略 '='
            'delimiter','\n');
        fclose(fileID);

        % break if no clippings
        if isempty(clippings)||length(clippings{1,1})<5
            warning('No clippings in your file %s',char(clipImportFile));
            return;
        end

        %% get every note
        % get ervery note by segClip.

        clippings = clippings{1,1};

        % Ignorant clipping if its content is not equal 4 lines.
        segIndex = strcmp(clippings,segClip);
        segIndex = find(segIndex==1);
        subSegIndex = segIndex(2:end) - segIndex(1:end-1);
        subSegIndex = [segIndex(1); subSegIndex] - 1;

        % the index of not four-line clippings.
        noneFourLine = find(subSegIndex~=4);

        if numel(noneFourLine)~=0
            % warning for ignorance lines.
            warning('Ignorant clippings in file %s',char(clipImportFile));
            for k=1:numel(noneFourLine)
                fprintf('	Clipping before line %g-th.\n',segIndex(noneFourLine(k)));
            end
            
            % delete none-four-lines clippings.
            segIndex = setdiff(segIndex,segIndex(noneFourLine));
            tempClip = cell(length(clippings)-sum(subSegIndex(noneFourLine))-...
                numel(noneFourLine),1);
            for i=1:numel(segIndex)
                [tempClip{(i-1)*5+1:i*5}] = deal(clippings{segIndex(i)-4:segIndex(i)});
            end
            clippings = tempClip;
        end

        % split bookname+author location+date clippping
        sizeClip = length(clippings)/5;
        clipText = cell(sizeClip,3);
        for i=1:3
            if i~=3
                [clipText{:,i}] = deal(clippings{i:5:end,1});
            else
                [clipText{:,i}] = deal(clippings{i+1:5:end,1});
            end
        end

        %% detail splitting
        % bookname author clipping clipping-style location time1 time2
        % time1 mm-dd-yy, time2 hh-mm-ss

        clipExport = cell(sizeClip,7);

        [clipExport{:,3}] = deal(clipText{:,3});    % save clippings

        for i=1:sizeClip
            % save bookname author
            % split by '('
            tempClip = clipText{i,1};
            indexAuthor = find(tempClip=='(');
            if ~isempty(indexAuthor)
                tempAuthor = tempClip(1:indexAuthor(end)-1);
                tempTitle = tempClip(indexAuthor(end)+1:end-1);
            else
                tempAuthor = '';
                tempTitle = tempClip;
            end
            
            clipExport{i,1} = tempTitle;            % save bookname
            clipExport{i,2} = tempAuthor;           % save author
            
            % save clipping-style
            % split by （'我的',' 位置',) or ('的',' |') or ('Your ',' at')
            % ('This ',' at') - Article
            tempClip = clipText{i,2};
            tempClipStyle = textscan(tempClip,'%s','delimiter',...
                {'我的',' 位置','的',' |','Your ',' at','This '});
            clipExport{i,4} = tempClipStyle{1,1}{2};
            
            % save location
            % if double page spread or more.
            tempLocation = regexp(tempClip,'(\d+)-(\d+)','tokens');
            % single page
            if isempty(tempLocation)
                tempLocation = regexp(tempClip,'(\d+)','tokens');
                tempLocation = tempLocation{1};
            else
                tempLocation = tempLocation{1,1};
                tempLocation = strcat(tempLocation{1},'-',tempLocation{2});
            end
            
            clipExport{i,5} = tempLocation;         % save location
            
            % save time yy-mm-dd hh-mm-ss
            % split by '添加于' or 'Added on' - time
            % split by ('年','月','日星期') or (', ') - time1 time2
            tempTime = textscan(tempClip,'%s','delimiter',{'添加于','Added on'});
            tempTime = tempTime{1,1};
            tempTime = tempTime{end};
            
            tempTime2 = regexp(tempTime,'(\d+):(\d+):(\d+)','tokens');
            tempTime2 = tempTime2{1,1};
            tempTime2ch = tempTime2;
            tempTime2 = time2str(tempTime2);        % save time2
            
            tempTimeSeg = textscan(tempTime,'%s',...
                'delimiter',{'年','月','日星期',','});
            if length(tempTimeSeg{1,1}) > 2         % Chinese-format
                tempTime12 = strrep(tempTime,tempTime2,'');
                tempTime12 = textscan(tempTime12,'%s','delimiter',{'年','月','日'});
                tempTime12 = tempTime12{1,1};
                
                tptempTime1 = cell(3,1);
                tptempTime1{1} = tempTime12{1};   % year
                % date month
                for zr=2:3
                    tptempTime1{zr} = tempTime12{zr};
                    if length(tptempTime1{zr,1})~=2
                        tptempTime1{zr} = strcat('0',tptempTime1{zr,1});
                    end
                end
                
                ampm = tempTime12{end,1};
                ampm = ampm(end-1:end);             % am pm
                if strcmp(ampm,'下午')
                    tempTime2ch{1} = num2str(str2double(tempTime2ch{1})+12);
                    tempTime2 = time2str(tempTime2ch);  % save time2
                end
                
                tempTime1 = date2str(tptempTime1);  % save time1
            else                                    % English-format
                tempTime1 = strrep(tempTime,tempTime2,'');
                tempTime1 = textscan(tempTime1,'%s','delimiter',',');
                tempTime1 = tempTime1{1,1}{2};
                tptempTime1{3,1} = tempTime1(1:2);          % date
                tptempTime1{2,1} = tempTime1(4:end-6);      % month
                tptempTime1{1,1} = tempTime1(end-4:end-1);  % year
                % convert month to num
                tptempTime1{2,1} = month2num(tptempTime1{2,1});
                tempTime1 = date2str(tptempTime1);          % save time1
            end
            
            clipExport{i,6} = tempTime1;                    % save time1
            clipExport{i,7} = tempTime2;                    % save time2
        end

        %% delete lines with no clippings

        tempNoClip = cell(sizeClip,1);
        [tempNoClip{:}] = deal(clipExport{:,3});
        tempNoClipIndex = strcmp(tempNoClip,'');
        tempWithClipIndex = setdiff(1:sizeClip,find(tempNoClipIndex==1));

        sizeClip = length(tempWithClipIndex);
        tempClip = cell(sizeClip,7);
        for k=1:sizeClip
            [tempClip{k,:}] = deal(clipExport{tempWithClipIndex(k),:});
        end
        clipExport = tempClip;

        %% varargout

        if nargout==1, varargout{1} = clipExport; end

        %% export txt-file
        % not available

        % fileWrite = fopen(clipExportFile,'a+','n',encoding);
        % formarSpec = {'> %s\n\n',...
        %     '<p text-align=right>%s # %s</p>\n'};
        % for i=117:137
        %     clipcontent = clipExport{i,dx(5)};
        %     cliplocation = clipExport{i,dx(3)};
        %     cliptime = clipExport{i,dx(4)};
        %     fprintf(fileWrite, '\n');
        %     fprintf(fileWrite, formarSpec{1}, clipcontent);
        %     fprintf(fileWrite, formarSpec{2}, cliplocation, cliptime);
        % end
        % fclose(fileWrite);

        %% subfunction

            function timestr = time2str(timehms)
                timestr = strcat(timehms{1},':',timehms{2},':',timehms{3});
            end

            function datestr = date2str(dateymr)
                datestr = strcat(dateymr{1},'-',dateymr{2},'-',dateymr{3});
            end

            function monthstr = month2num(monthorigin)
                switch monthorigin
                    case 'January', monthstr = '01';
                    case 'February', monthstr = '02';
                    case 'March', monthstr = '03';
                    case 'April', monthstr = '04';
                    case 'May', monthstr = '05';
                    case 'June', monthstr = '06';
                    case 'July', monthstr = '07';
                    case 'August', monthstr = '08';
                    case 'September', monthstr = '09';
                    case 'October', monthstr = '10';
                    case 'November', monthstr = '11';
                    case 'December', monthstr =  '12';
                    otherwise, monthstr = monthorigin;
                end
            end

        end


###资源

- [unkeltao-kindle-note-format](http://www.unkeltao.com/blog/2014/03/14/kindlebi-ji-zhuan-huan/)
- [kindleclippings](http://www.ruby-doc.org/gems/docs/k/kindleclippings-1.3.2/README_markdown.html)
- [Kindle-Clippings-Export](https://github.com/rydjones/Kindle-Clippings-Export)
- [klipbook](https://github.com/grassdog/klipbook)
- [kindle-clips](https://github.com/minejo/kindle-clips)
- [kindle-clippings](https://github.com/lxyu/kindle-clippings)