title: "Xhprof安装与使用"
date: 2015-05-28 01:01:40
categories: PHP
tags: PHP
---


### 简介
 *Xhprof能用来做什么？*
    XHProf是一个分层PHP性能分析工具。它报告函数级别的请求次数和各种指标，包括阻塞时间，CPU时间和内存使用情 况。一个函数的开销，可细分成调用者和被调用者的开销。
   
### Xhprof 安装
* Xhprof安装
       wget http://pecl.php.net/get/xhprof-0.9.2.tgz 
       tar xzvf xhprof-0.9.2.tgz 
       cd xhprof-0.9.2/extension/ 
       cp -r xhprof_html xhprof_lib /usr/local/www/ 
       /usr/local/php/bin/phpize 
       ./configure --with-php-config=/usr/local/php/bin/php-config 
       make  
       make install 
	
	修改php.ini，添加xhprof.so （*注意xhprof.so需要在extension_dir目录下*）
        extension=xhprof.so   
        xhprof.output_dir=/var/logs/xhprof 

* graphviz安装（*性能数据也可以通过callgraph视图来查看 。callgraph 会高亮显示程序的关键路径。*）
        wget http://www.graphviz.org/pub/graphviz/stable/SOURCES/graphviz-2.24.0.tar.gz
        tar zxf graphviz-2.24.0.tar.gz
        cd graphviz-2.24.0
        编译安装
        ./configure
        make
        make install
        
### Xhprof 使用
* XHProf.class.php（*本事例是将xhprof_html xhprof_lib XHProf.class.php demo.php放在同一级目录下面，需要web程序能够访问到*）
		
		class XHProf {
	        public function __construct() {
	            // start profiling
	            include_once "./xhprof_lib/utils/xhprof_lib.php";
	            include_once "./xhprof_lib/utils/xhprof_runs.php";
	        }
	    
	        public function beginProf() {
	            xhprof_enable(XHPROF_FLAGS_CPU + XHPROF_FLAGS_MEMORY);
	        }
	    
	        public function endProf() {
	            $xhprof_data = xhprof_disable();
	    
	            $xhprof_runs = new XHProfRuns_Default();
	            $run_id = $xhprof_runs->save_run($xhprof_data, "xhprof_foo");
	    
	            echo "<a href=\"http://127.0.0.1/xhprof_html/index.php?run=$run_id&source=xhprof_foo\">性能分析结果</a>";
	        }
    
    
* demo.php
    
	    ini_set('display_errors', 1);
	    include './XHProf.class.php';
	    $objProf = new XHProf();
	    
	    function foo() {
	        echo 'hello world';
	    }
	    
	    //开启xhprof并开始记录
	    $objProf->beginProf();
	    
	    //运行一些函数
	    foo();
	    
	    //停止记录并取到结果
	    $objProf->endProf();