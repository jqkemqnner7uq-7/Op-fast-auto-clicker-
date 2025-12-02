javascript:(function(){
  var i=0;
  function c(x,y){
    var e=document.elementFromPoint(x,y);
    if(!e)return;
    var down=new MouseEvent('mousedown',{bubbles:true,cancelable:true,clientX:x,clientY:y,buttons:1});
    var up=new MouseEvent('mouseup',{bubbles:true,cancelable:true,clientX:x,clientY:y});
    var click=new MouseEvent('click',{bubbles:true,cancelable:true,clientX:x,clientY:y});
    e.dispatchEvent(down);
    e.dispatchEvent(up);
    e.dispatchEvent(click);
  }
  function f(){
    if(!window.ac_running)return;
    var x=window.ac_x,y=window.ac_y;
    c(x,y);
    i++;
    requestAnimationFrame(f);
  }
  document.onmousemove=function(e){
    window.ac_x=e.clientX;
    window.ac_y=e.clientY;
  };
  if(window.ac_running){
    window.ac_running=false;
    clearInterval(window.ac_interval);
    alert('Auto-clicker OFF ('+i+' clicks)');
  }else{
    window.ac_running=true;
    i=0;
    alert('Auto-clicker ON - Move mouse to stop clicking');
    f();
  }
})();
