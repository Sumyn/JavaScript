var EventUtil={
    addHandler: function (element, type, handler) {
        if(element.addEventListener){
            element.addEventListener(type,handler,false);
        }else if(element.attachEvent){
            element.attachEvent("on"+type,handler);
        }else{
            element["on"+type]=handler;
        }
    },
    getEvent: function (event) {
        return event ? event : window.event; //返回对event对象的引用
    },
    getTarget: function (event) {
        return event.target || event.srcElement; //返回事件的目标
    },
    preventDefault: function (event) { //取消事件的默认行为
        if(event.preventDefault){
            event.preventDefault();
        }else{
            event.returnValue=false;
        }
    },
    removeHandler: function (element, type, handler) {
        if(element.removeEventListener){
            element.removeEventListener(type,handler,false);
        }else if(element.detachEvent){
            element.detachEvent("on"+type,handler);
        }else{
            element["on"+type]=null;
        }
    },
    stopPropagation: function (event) {
        if(event.stopPropagation){
            event.stopPropagation();
        }else{
            event.cancelBubble=true;
        }
    },
    getClipboardText: function (event) {
        var clipboardData=(event.clipboardData || window.clipboardData);
        return clipboardData.getData("text");
    },
    setClipboardText: function (event,value) {
        if(event.clipboardData){
            return event.clipboardData.setData("text/plain",value);
        }else if(window.clipboardData){
            return window.clipboardData.setData("text",value);
        }
    }
};
