<script lang="ts">
	import Button, { Label, Icon } from '@smui/button';

	let clicked = 0;

	function handleClick(event: CustomEvent | MouseEvent) {
		event = event as MouseEvent;
		if (event.button === 0) {
			clicked = clicked + 2;
		}
	}

	function reset() {
		clicked = 1;
	}
</script>

<Button on:mousedown={handleClick}>
	<Icon class="material-icons">thumb_up</Icon>
	<Label>Click Me</Label>
</Button>
<Button href="/profile">
	<Icon class="material-icons">thumb_up</Icon>
	<Label>ir a perfil</Label>
</Button>
{@html '<!DOCTYPE html><html><head><meta charset="utf-8"><script src="https://cdn.jsdelivr.net/npm/@mediapipe/camera_utils/camera_utils.js" crossorigin="anonymous"></script><script src="https://cdn.jsdelivr.net/npm/@mediapipe/control_utils/control_utils.js" crossorigin="anonymous"></script><script src="https://cdn.jsdelivr.net/npm/@mediapipe/control_utils_3d/control_utils_3d.js" crossorigin="anonymous"></script><script src="https://cdn.jsdelivr.net/npm/@mediapipe/drawing_utils/drawing_utils.js" crossorigin="anonymous"></script><script src="https://cdn.jsdelivr.net/npm/@mediapipe/pose/pose.js" crossorigin="anonymous"></script></head><body><div class="container"><video class="input_video"></video><canvas class="output_canvas" width="1280px" height="720px"></canvas><div class="landmark-grid-container"></div></div></body> <script>const videoElement = document.getElementsByClassName("input_video")[0];const canvasElement = document.getElementsByClassName("output_canvas")[0];const canvasCtx = canvasElement.getContext("2d");const landmarkContainer = document.getElementsByClassName("landmark-grid-container")[0];const grid = new LandmarkGrid(landmarkContainer);function onResults(results) {if (!results.poseLandmarks) {grid.updateLandmarks([]);return;}canvasCtx.save();canvasCtx.clearRect(0, 0, canvasElement.width, canvasElement.height);canvasCtx.drawImage(results.segmentationMask, 0, 0,canvasElement.width, canvasElement.height);canvasCtx.globalCompositeOperation = "source-in";canvasCtx.fillStyle = "#00FF00";canvasCtx.fillRect(0, 0, canvasElement.width, canvasElement.height);canvasCtx.globalCompositeOperation = "destination-atop";canvasCtx.drawImage(results.image, 0, 0, canvasElement.width, canvasElement.height);canvasCtx.globalCompositeOperation = "source-over";drawConnectors(canvasCtx, results.poseLandmarks, POSE_CONNECTIONS,{color: "#00FF00", lineWidth: 4});drawLandmarks(canvasCtx, results.poseLandmarks,{color: "#FF0000", lineWidth: 2});canvasCtx.restore();grid.updateLandmarks(results.poseWorldLandmarks);}const pose = new Pose({locateFile: (file) => {return `https://cdn.jsdelivr.net/npm/@mediapipe/pose/${file}`;}});pose.setOptions({modelComplexity: 1,smoothLandmarks: true,enableSegmentation: true,smoothSegmentation: true,minDetectionConfidence: 0.5,minTrackingConfidence: 0.5});pose.onResults(onResults);const camera = new Camera(videoElement, {onFrame: async () => {await pose.send({image: videoElement});},width: 1280,height: 720});camera.start();</script></html>'}
<p class="mdc-typography--body1">
	{#if clicked}
		You've clicked the button {clicked} time{clicked === 1 ? '' : 's'}. You can
		<a on:click={reset} href="javascript:void(0);">reset it</a>.
	{:else}
		<span class="grayed">You haven't clicked the button.</span>
	{/if}
</p>

<style>
	.grayed {
		opacity: 0.6;
	}
</style>
