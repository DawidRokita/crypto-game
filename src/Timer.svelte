<script>
    import { onInterval } from "./utils.js";
    export let callback;
    export let interval = 500;
    onInterval(callback, interval);
</script>
