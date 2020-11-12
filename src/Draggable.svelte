<script>
    // 1) Create a component name Draggable
    // 2) Create a section with an class dragable
    // 3) Add a border around draggable with cursor move and also absolute position the section
    // 4) Add a slot inside draggable to make it so other components can use it
    // 5) Add the window component
    // 6) Add a variable named moving and set it to false
    // 7) Add 2 export variables top and left.  I will default mine to 300, 300.
    // 8) Use those variables to control the position 
    // 9) Add a mouse down event to the section to know when the mouse is down.  Set the moving to true.
    // 10) Add a mousemove event to window to trigger moving; use the movementX and movementY to control add to the left and top variables if the it's moving
    // 11) Add a on mouse up event to the window turn off dragging
    export let left = 300;
    export let top = 300;
    let moving = false;

    function onMouseDown() {
        moving = true;
        console.log('moving');
    }
    function onMove(e) {
        if (moving) {
            top += e.movementY;
            left += e.movementX;
        }
    }

    function onMouseUp() {
        moving = false;
    }
</script>

<style>
    .draggable {
        border: solid gray 1px;
        cursor: move;
        position: absolute;
        user-select: none;
    }
</style>


<section on:mousedown={onMouseDown} style="left: {left}px; top: {top}px;" class="draggable">
    <slot></slot>
</section>

<svelte:window on:mouseup={onMouseUp} on:mousemove={onMove}  />