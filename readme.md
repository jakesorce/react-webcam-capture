# react-webcam-capture
react-webcam-capture is module for capturing multimedia from WebBrowser via React.
It uses navigator.mediaDevices.getUserMedia and MediaRecorder API, so make sure that your browser supports.


## Install
`yarn add react-webcam-capture`

## Features
- Uses supporting getUserMedia API from mediaDevices.getUserMedia/getUserMedia/-vendor_prefix-GetUserMedia.
- Easy, intuitive interface
- Video Recording
- Audio Recording
- Supports Pausing & Resuming

## Example

### VideoRecorder Example

```javascript

import ReactWebCamCapture from 'react-webcam-capture';

class VideoExample extends Component {
  ...
  render() {
    return (
      <div ref='app'>
        ...
        <h1>Video Recording Example</h1>
        <hr />

        <ReactWebCamCapture
          constraints={{ audio: true, video: true }}
          timeSlice={10}
          onGranted={this.handleGranted}
          onDenied={this.handleDenied}
          onStart={this.handleStart}
          onStop={this.handleStop}
          onPause={this.handlePause}
          onResume={this.handleResume}
          onError={this.handleError}
          render={({ start, stop, pause, resume }) =>
          <div>
            <p>Granted: {granted.toString()}</p>
            <p>Rejected Reason: {rejectedReason}</p>
            <p>Recording: {recording.toString()}</p>
            <p>Paused: {paused.toString()}</p>

            <button onClick={start}>Start</button>
            <button onClick={stop}>Stop</button>
            <button onClick={pause}>Pause</button>
            <button onClick={resume}>Resume</button>

            <p>Streaming test</p>
            <video autoPlay></video>
          </div>
        } />
      </div>
    );
  }
}

```

## Props

### Object constraints
Set the getUserMedia constraints. Default is { video: true, audio: true }.

### String className
Set the class name of the element.

### String mimeType
Set mimeType for MediaRecorder API. It uses 'video/webm;codecs=vp8' by default. If you are trying to record Audio, you should use 'audio/webm' instead.

### Number timeSlice (default 10)
Set time slice of [mediaRecorder.start](https://developer.mozilla.org/en-US/docs/Web/API/MediaRecorder/start).

### Function onGranted
Handler that fires on browser acquired permission to access media devices.

### Function onDenied(Error err)
Handler that fires on browser denied permission to access media devices.

### Function onStart(MediaStream stream)
Handler that fires on user started recording.

### Function onStop
Handler that fires on user stopped recording.

### Function onPause
Handler that fires on user paused recording.

### Function onResume(MediaStream stream)
Handler that fires on user resumed recording.

### Function onError(Error err)
Handler that fires on error occurs. This also could be fired if the browser not support getUserMedia and mediaRecorder API.

### Function render({ start, stop, pause, resume })
Render the child components with functions. Each function actually manipulate recording related jobs into parent like VideoRecorder or AudioRecorder.
