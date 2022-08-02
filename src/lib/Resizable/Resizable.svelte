<script>
// @ts-nocheck
 
    

    let isResizing = false;
    function mousedown(e) {
      window.addEventListener("mousemove", (e) => mousemove(e));
      window.addEventListener("mouseup", mouseup);
      let prevX = e.clientX;
      let prevY = e.clientY;
      function mousemove(e) {
        if (!isResizing) {
          let newX = prevX - e.clientX;
          let newY = prevY - e.clientY;
    
          const rect = el.getBoundingClientRect();
    
          el.style.left = rect.left - newX + "px";
          el.style.top = rect.top - newY + "px";
    
          prevX = e.clientX;
          prevY = e.clientY;
        }
      }
    
      function mouseup() {
        window.removeEventListener("mousemove", mousemove);
        window.removeEventListener("mouseup", mouseup);
      }
    }
    
    let currentResizer;


    
      function resizedown(e) {
        currentResizer = e.target;
        isResizing = true;
    
        let prevX = e.clientX;
        let prevY = e.clientY;
    
        window.addEventListener("mousemove", mousemove);
        window.addEventListener("mouseup", mouseup);
    
        function mousemove(e) {
            const rect = el.getBoundingClientRect();
            el.style.width = rect.width - (prevX - e.clientX) + "px";
            el.style.height = rect.height - (prevY - e.clientY) + "px";
            prevX = e.clientX;
            prevY = e.clientY;
        }
    
        function mouseup() {
          window.removeEventListener("mousemove", mousemove);
          window.removeEventListener("mouseup", mouseup);
          isResizing = false;
        }
    }
    
    </script>


<div class="resize-continer" on:mousedown={(e) => mousedown(e)}>
    <div class="resize-content-well">
        <slot></slot>
    </div>
    <span class="resizer" on:mousedown={(e) => resizedown(e)}>&xharr;</span>
</div>


<style>



.resizer {
    transform: rotate(45deg);
    position: absolute;
    width: 10px;
    height: 10px;
    color: red;
    border: solid 2px salmon;
}


</style>