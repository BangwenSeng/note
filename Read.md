# note



##    监控微信返回按钮
    $(function(){  
    pushHistory();  
    window.addEventListener("popstate", function(e) {  
        alert("我监听到了浏览器的返回按钮事件啦");//根据自己的需求实现自己的功能  
    }, false);  
        function pushHistory() {  
            var state = {  
                title: "title",  
                url: "#"  
            };  
            window.history.pushState(state, "title", "#");  
        }  
          
    });  
## datetimepicker 日期使用方法
	var $startVl;
        var $endVl;
        var $date = new Date();
        var $currentTime = $date.toLocaleDateString();
        //配置中文日期
        $.fn.datetimepicker.dates['zh-CN'] = {
            days: ["星期日", "星期一", "星期二", "星期三", "星期四", "星期五", "星期六", "星期日"],
            daysShort: ["周日", "周一", "周二", "周三", "周四", "周五", "周六", "周日"],
            daysMin: ["日", "一", "二", "三", "四", "五", "六", "日"],
            months: ["一月", "二月", "三月", "四月", "五月", "六月", "七月", "八月", "九月", "十月", "十一月", "十二月"],
            monthsShort: ["一月", "二月", "三月", "四月", "五月", "六月", "七月", "八月", "九月", "十月", "十一月", "十二月"],
            today: "现在",
            suffix: [],
            meridiem: ["上午", "下午"]
        };

        $('#start').datetimepicker({
            minView: "month",
            format: 'yyyy-mm-dd',
            language: 'zh-CN',
            autoclose: true,
            todayBtn: false,
            endDate: $currentTime
        }).on('changeDate',function(ev){
          var starttime=$("#start").val();
          var endtime=$("#end").val();
          $("#end").datetimepicker('setStartDate',starttime);
          $("#start").datetimepicker('hide');
        });

        function endTime($startTime) {
         
            $('#end').datetimepicker({
                minView: "month",
                format: 'yyyy-mm-dd',
                language: 'zh-CN',
                autoclose: true,
                todayBtn: true,
                startDate: $startTime,
                endDate: $currentTime
            }).on('changeDate',function(ev){
               var starttime=$("#start").val();
               var endtime=$("#end").val();
               $("#start").datetimepicker('setEndDate',endtime);
               $("#end").datetimepicker('hide');

              });
        }
        /**$('#end') 为结束日期的input
        $('#start') 为开始日期的Input
        **/
        $(function () {
           $startVl = $('#start').val(); //关键 类似Init 如果不设置,日期会变英文
           endTime($startVl);
        });

        $('#end').focus(function () {

            $startVl = $('#start').val();

            endTime($startVl);

            $('#end').datetimepicker('show');

        });
        // $('#submit').blur(function () {
        //     $('#start-hint').hide();
        // });


        $('#submit').click(function () {

            table.draw();  //这个不是日期，但和异步datatable有关
            				重新筛选条件用ajax请求一边
           
        });
