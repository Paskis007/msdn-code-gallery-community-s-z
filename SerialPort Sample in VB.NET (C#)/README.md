# SerialPort Sample in VB.NET (C#)
## Requires
- Visual Studio 2008
## License
- Apache License, Version 2.0
## Technologies
- Windows Forms
- threading
- SerialPort
## Topics
- SerialPort class
## Updated
- 07/30/2012
## Description

<h1><span><span style="font-size:large"><strong><span style="font-size:large">
<p style="padding-left:30px">Introduction</p>
<p style="padding-left:30px"><span style="font-size:x-small">My sample demonstrates the usage of SerialPort class based on my own expereriences. I will show how You can effective use the SerialPort Datareceived event handle</span></p>
<p style="padding-left:30px"><span><span style="font-size:large"><strong><span style="font-size:large"><span style="font-size:x-small">Please notice my other contribution(s) with SerialPort</span></span></strong></span></span></p>
<p style="padding-left:30px"><span><span style="font-size:large"><strong><span style="font-size:large"><span style="font-size:x-small"><br>
<a href="http://code.msdn.microsoft.com/SerialPort-Windows-Forms-a43f208e">http://code.msdn.microsoft.com/SerialPort-Windows-Forms-a43f208e</a></span></span></strong></span></span></p>
<p style="padding-left:30px"><span><span style="font-size:large"><strong><span style="font-size:large"><span><span style="font-size:large"><strong><span style="font-size:large"><span style="font-size:x-small"><a href="http://code.msdn.microsoft.com/Extended-SerialPort-10107e37">http://code.msdn.microsoft.com/Extended-SerialPort-10107e37</a></span></span></strong></span></span></span></strong></span></span></p>
</span></strong>
<p style="padding-left:30px">Building the Sample</p>
</span></span></h1>
<p style="padding-left:30px">The only neccessary requirement is a COM port on Your System. It may me also a USB serial device. To run this sample You need two computers connected with a null modem cable. Install this sample on both or use hyperterminal on one
 side.</p>
<p style="padding-left:30px"><span style="font-size:xx-small">&nbsp;</span><strong><span style="font-size:large">The user interface</span></strong></p>
<p><span style="font-family:Lucida Console; font-size:large"><span style="font-family:Lucida Console; font-size:large">&nbsp;<img src="http://i1.code.msdn.s-msft.com/serialport-sample-in-vbnet-fb040fb2/image/file/57810/1/sc.bmp" alt="" width="530" height="122"></span></span>&nbsp;</p>
<ul>
<li>choose a Com on combobox &quot;Port&quot; </li><li>choose baudrate on combobox &quot;Baud&quot; </li><li>press button &quot;Open Port&quot; </li><li>enter a message in the TX box </li><li>press button &quot;send ...&quot; </li><li>use button array on left side to send one character </li><li>send a messsage from remote </li><li>press button &quot;Close Port&quot; when Your session is finished </li></ul>
<p>&nbsp;</p>
<h1 style="padding-left:30px"><span style="font-size:large">Walk thrue the code</span></h1>
<p style="padding-left:30px">When the application starts it will retrieve all available COM ports from the System. Be aware that the array Portnames is nothing, when no port on system exists.</p>
<p>&nbsp;</p>
<p>&nbsp;<strong>Portnames from System</strong></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Skript bearbeiten</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span>

<div class="preview">
<pre class="vb">&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'''&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'''&nbsp;open&nbsp;Windows&nbsp;Form</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'''&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;Form1_Load(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.EventArgs.aspx" target="_blank" title="Auto generated link to System.EventArgs">System.EventArgs</a>)&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;<span class="visualBasic__keyword">MyBase</span>.Load&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;read&nbsp;avaiable&nbsp;COM&nbsp;Ports:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Dim</span>&nbsp;Portnames&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">String</span>()&nbsp;=&nbsp;System.IO.Ports.SerialPort.GetPortNames&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;Portnames&nbsp;<span class="visualBasic__keyword">Is</span>&nbsp;<span class="visualBasic__keyword">Nothing</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(<span class="visualBasic__string">&quot;There&nbsp;are&nbsp;no&nbsp;Com&nbsp;Ports&nbsp;detected!&quot;</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Me</span>.Close()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cboComPort.Items.AddRange(Portnames)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cboComPort.Text&nbsp;=&nbsp;Portnames(<span class="visualBasic__number">0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cboBaudRate.Text&nbsp;=&nbsp;<span class="visualBasic__string">&quot;9600&quot;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p>&nbsp;<strong>Initialize Serialport properties</strong></p>
<p style="padding-left:30px">Here are standard settings to communicate in text format.</p>
<p>.ParityReplace replaces an incoming char with the given value (&quot;;&quot;), when a parity error occurs. In this example it has no effect because I use parity none.</p>
<p>.RecevedBytesThreshold default = 1 means that when one byte is received the Datareceived event will be fired. See later notices</p>
<p>.NewLine is used in Serailport.ReadLine method. This given character terminates a readline and assigns the content to local variable. Notice when You use .SendLine method this character will be added automatically. Some protocols use STX,ETX flow control.
 You may set this property to one of this values.</p>
<p>.ReadTimeout When on data frame has not yet finished after 10000ms a exception will occur. You can handle now hanging communication. Please try it: Send a Char to app without carriage return. After 10000 ms a TimeOutException will occur</p>
<p style="padding-left:30px">&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Skript bearbeiten</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span>

<div class="preview">
<pre class="vb">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;device&nbsp;params</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">With</span>&nbsp;SerialPort1&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.ParityReplace&nbsp;=&nbsp;&amp;H3B&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;replace&nbsp;&quot;;&quot;&nbsp;when&nbsp;parity&nbsp;error&nbsp;occurs</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.PortName&nbsp;=&nbsp;cboComPort.Text&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.BaudRate&nbsp;=&nbsp;<span class="visualBasic__keyword">CInt</span>(cboBaudRate.Text)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.Parity&nbsp;=&nbsp;IO.Ports.Parity.None&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.DataBits&nbsp;=&nbsp;<span class="visualBasic__number">8</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.StopBits&nbsp;=&nbsp;IO.Ports.StopBits.One&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.Handshake&nbsp;=&nbsp;IO.Ports.Handshake.None&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.RtsEnable&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.ReceivedBytesThreshold&nbsp;=&nbsp;<span class="visualBasic__number">1</span>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'threshold:&nbsp;one&nbsp;byte&nbsp;in&nbsp;buffer&nbsp;&gt;&nbsp;event&nbsp;is&nbsp;fired</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.NewLine&nbsp;=&nbsp;vbCr&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;CR&nbsp;must&nbsp;be&nbsp;the&nbsp;last&nbsp;char&nbsp;in&nbsp;frame.&nbsp;This&nbsp;terminates&nbsp;the&nbsp;SerialPort.readLine</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;.ReadTimeout&nbsp;=&nbsp;<span class="visualBasic__number">10000</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">With</span>&nbsp;
</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p>&nbsp;&nbsp;</p>
<p style="padding-left:30px"><strong>Open the COM port</strong></p>
<p style="padding-left:30px">I suggest in any cases embedding the method into a Try .. Catch. Indeed this is the only way to find out whether the port is already used by another application</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Skript bearbeiten</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span>

<div class="preview">
<pre class="vb">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;check&nbsp;whether&nbsp;device&nbsp;is&nbsp;avaiable:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.Open()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;comOpen&nbsp;=&nbsp;SerialPort1.IsOpen&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Catch</span>&nbsp;ex&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Exception&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;comOpen&nbsp;=&nbsp;<span class="visualBasic__keyword">False</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(<span class="visualBasic__string">&quot;Error&nbsp;Open:&nbsp;&quot;</span>&nbsp;&amp;&nbsp;ex.Message)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p><strong>&nbsp;Reading COM port</strong></p>
<p><strong>&nbsp;</strong></p>
<p><strong>Please notice: To run this sample successfully external device MUST send a carriage return at the end of every frame</strong></p>
<p>A great misunderstanding of all beginners in Serialport is the usage of the Datareceived event handle. The handle method seems to be a normal member of the class. But in fact this is a secondary thread. Therefore You have to follow the rules of Threading.
 You retrieve a &quot;illegal crossthreaderror&quot; message when You try to write data direct to one UI control of Your Form. This is the correct way to achieve this:</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span>

<div class="preview">
<pre class="vb">&nbsp;<span class="visualBasic__com">'''&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'''&nbsp;async&nbsp;read&nbsp;on&nbsp;secondary&nbsp;thread</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'''&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Private</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;SerialPort1_DataReceived(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;System.<span class="visualBasic__keyword">Object</span>,&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.IO.Ports.SerialDataReceivedEventArgs.aspx" target="_blank" title="Auto generated link to System.IO.Ports.SerialDataReceivedEventArgs">System.IO.Ports.SerialDataReceivedEventArgs</a>)&nbsp;_&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Handles</span>&nbsp;SerialPort1.DataReceived&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;comOpen&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;readBuffer&nbsp;=&nbsp;SerialPort1.ReadLine()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'data&nbsp;to&nbsp;UI&nbsp;thread</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Me</span>.Invoke(<span class="visualBasic__keyword">New</span>&nbsp;EventHandler(<span class="visualBasic__keyword">AddressOf</span>&nbsp;DoUpdate))&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Catch</span>&nbsp;ex&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;Exception&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;MsgBox(<span class="visualBasic__string">&quot;read&nbsp;&quot;</span>&nbsp;&amp;&nbsp;ex.Message)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'''&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'''&nbsp;update&nbsp;received&nbsp;string&nbsp;in&nbsp;UI</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'''&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">Public</span>&nbsp;<span class="visualBasic__keyword">Sub</span>&nbsp;DoUpdate(<span class="visualBasic__keyword">ByVal</span>&nbsp;sender&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<span class="visualBasic__keyword">Object</span>,&nbsp;<span class="visualBasic__keyword">ByVal</span>&nbsp;e&nbsp;<span class="visualBasic__keyword">As</span>&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.EventArgs.aspx" target="_blank" title="Auto generated link to System.EventArgs">System.EventArgs</a>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tbRx.Text&nbsp;=&nbsp;readBuffer&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">Sub</span></pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p>&nbsp;</p>
<p>&nbsp;<strong>Close the COM port</strong></p>
<p>&nbsp;<strong>&nbsp;</strong>I suggest in any cases to clear the input buffer before You execute the .Close method</p>
<p style="padding-left:30px">&nbsp;</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>Visual Basic</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Skript bearbeiten</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">vb</span>

<div class="preview">
<pre class="vb">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;comOpen&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__com">'&nbsp;clear&nbsp;input&nbsp;buffer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.DiscardInBuffer()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.Close()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="visualBasic__keyword">End</span>&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;
</pre>
</div>
</div>
</div>
<p>&nbsp;</p>
<p><strong>&nbsp;</strong><strong>&nbsp; </strong></p>
<p><strong>Timing: How quick is the Datareceived event?</strong></p>
<p>I have tested this on a XP System 32 bit, 1,7 Ghz, no other application running. I have placed a SerialPort.Write into the event handle. The .RecevedBytesThreshold is 1. Here is the result:</p>
<p><strong>&nbsp;</strong></p>
<p>&nbsp;</p>
<div class="endscriptcode">
<div class="endscriptcode">&nbsp;<img src="http://i1.code.msdn.s-msft.com/serialport-sample-in-vbnet-fb040fb2/image/file/56933/1/serialportresponse.jpg" alt="" width="600" height="247"></div>
<p>&nbsp;</p>
<p>External device (mcu) sends STX (02). The dataReceived handle responses direct with a frame of bytes.</p>
<p>In free running mode the timespan is jittering between 4 - 6 ms. (Interval A-B on logic analyser) What is the conclusion of this fact? Try to fetch more bytes at once. You can use the inputbuffer with a default value 4096.</p>
<p>When You set .ReceivedBytesThreshold = 100 You will fetch up to 100 bytes at once. So You can tune the timing according to the baudrate. Another tuning trick is to make the event handle slower!</p>
<p>Place thread.Sleep(xx) in the event handle directly before You read the data. The effect is You application is quicker.</p>
<h1>Summary</h1>
<p>I think now it is very clear to everyone, that this property does not fetch the correct number of bytes in any cases. You cannot not trust this value, because the communication is still running and read the data is a little bit later.</p>
<p>Please download my sample and make Your own experiments. The Serialport is a very interesting class. With this class I started learning NET programming</p>
<p>A very useful article from Karsten: <a href="http://www.innovatic.dk/knowledg/SerialCOM/SerialCOM.htm">
http://www.innovatic.dk/knowledg/SerialCOM/SerialCOM.htm</a></p>
<h1>Appendix (from msdn)</h1>
<div class="sectionblock"><a id="remarksToggle"></a>
<p><span id="mt2" class="sentence">Serial received events can be caused by any of the items in the
<span><a href="http://msdn.microsoft.com/de-de/library/system.io.ports.serialdata.aspx">SerialData</a></span> enumeration.</span>
<span id="mt3" class="sentence">Because the operating system determines whether to raise this event or not, not all parity errors may be reported.</span></p>
<p><span id="mt4" class="sentence"><span><a href="http://msdn.microsoft.com/de-de/library/system.io.ports.serialport.pinchanged.aspx">PinChanged</a></span>,
<span><span class="selflink">DataReceived</span></span>, and <span><a href="http://msdn.microsoft.com/de-de/library/system.io.ports.serialport.errorreceived.aspx">ErrorReceived</a></span> events may be called out of order, and there may be a slight delay
 between when the underlying stream reports the error and when the event handler is executed.</span>
<span id="mt5" class="sentence">Only one event handler can execute at a time.</span></p>
<p><span id="mt6" class="sentence">The <span><span class="selflink">DataReceived</span></span> event is not guaranteed to be raised for every byte received.</span>
<span id="mt7" class="sentence">Use the <span><a href="http://msdn.microsoft.com/de-de/library/system.io.ports.serialport.bytestoread.aspx">BytesToRead</a></span> property to determine how much data is left to be read in the buffer.</span></p>
<p><span id="mt8" class="sentence">The <span><span class="selflink">DataReceived</span></span> event is raised on a secondary thread when data is received from the
<span><a href="http://msdn.microsoft.com/de-de/library/system.io.ports.serialport.aspx">SerialPort</a></span> object.</span>
<span id="mt9" class="sentence">Because this event is raised on a secondary thread, and not the main thread, attempting to modify some elements in the main thread, such as UI elements, could raise a threading exception.</span>
<span id="mt10" class="sentence">If it is necessary to modify elements in the main
<span><a href="http://msdn.microsoft.com/de-de/library/system.windows.forms.form.aspx">Form</a></span> or
<span><a href="http://msdn.microsoft.com/de-de/library/system.windows.forms.control.aspx">Control</a></span>, post change requests back using
<span><a href="http://msdn.microsoft.com/de-de/library/system.windows.forms.control.invoke.aspx">Invoke</a></span>, which will do the work on the proper thread.</span></p>
<p><span id="mt11" class="sentence">For more information about handling events, see
<span><a href="http://msdn.microsoft.com/de-de/library/2ccyd347.aspx">Consuming Events</a></span>.</span></p>
</div>
<p>&nbsp;</p>
<h1>Code C#</h1>
<p>&nbsp;&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Skript bearbeiten</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>

<div class="preview">
<pre class="csharp"><span class="cs__keyword">using</span>&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/Microsoft.VisualBasic.aspx" target="_blank" title="Auto generated link to Microsoft.VisualBasic">Microsoft.VisualBasic</a>;&nbsp;
<span class="cs__keyword">using</span>&nbsp;System;&nbsp;
<span class="cs__keyword">using</span>&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.Collections.aspx" target="_blank" title="Auto generated link to System.Collections">System.Collections</a>;&nbsp;
<span class="cs__keyword">using</span>&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.Collections.Generic.aspx" target="_blank" title="Auto generated link to System.Collections.Generic">System.Collections.Generic</a>;&nbsp;
<span class="cs__keyword">using</span>&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.Data.aspx" target="_blank" title="Auto generated link to System.Data">System.Data</a>;&nbsp;
<span class="cs__keyword">using</span>&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.Diagnostics.aspx" target="_blank" title="Auto generated link to System.Diagnostics">System.Diagnostics</a>;&nbsp;
&nbsp;
<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
<span class="cs__com">///&nbsp;Serial&nbsp;Port&nbsp;Demo&nbsp;Ellen&nbsp;Ramcke&nbsp;2012</span>&nbsp;
<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
<span class="cs__com">///&nbsp;&lt;remarks&gt;&lt;/remarks&gt;</span>&nbsp;
<span class="cs__keyword">public</span>&nbsp;<span class="cs__keyword">class</span>&nbsp;mainForm&nbsp;
{&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">string</span>&nbsp;readBuffer&nbsp;=&nbsp;<span class="cs__keyword">string</span>.Empty;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">int</span>&nbsp;Bytenumber;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">int</span>&nbsp;ByteToRead;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">char</span>[]&nbsp;byteEnd&nbsp;=&nbsp;<span class="cs__keyword">new</span>&nbsp;<span class="cs__keyword">char</span>[<span class="cs__number">3</span>];&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">bool</span>&nbsp;comOpen;<span class="cs__preproc">&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;#region&nbsp;&quot;form&nbsp;events</span>&quot;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;close&nbsp;application&nbsp;and&nbsp;COM&nbsp;Port</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Form1_FormClosed(System.Object&nbsp;sender,&nbsp;System.Windows.Forms.FormClosedEventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(comOpen)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.Close();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;open&nbsp;Windows&nbsp;Form</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Form1_Load(System.Object&nbsp;sender,&nbsp;System.EventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;read&nbsp;avaiable&nbsp;COM&nbsp;Ports:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">string</span>[]&nbsp;Portnames&nbsp;=&nbsp;<a class="libraryLink" href="http://msdn.microsoft.com/en-US/library/System.IO.Ports.SerialPort.GetPortNames.aspx" target="_blank" title="Auto generated link to System.IO.Ports.SerialPort.GetPortNames">System.IO.Ports.SerialPort.GetPortNames</a>();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(Portnames&nbsp;==&nbsp;<span class="cs__keyword">null</span>)&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Interaction.MsgBox(<span class="cs__string">&quot;There&nbsp;are&nbsp;no&nbsp;Com&nbsp;Ports&nbsp;detected!&quot;</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.Close();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cboComPort.Items.AddRange(Portnames);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cboComPort.Text&nbsp;=&nbsp;Portnames[<span class="cs__number">0</span>];&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cboBaudRate.Text&nbsp;=&nbsp;<span class="cs__string">&quot;9600&quot;</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;Open&nbsp;Com&nbsp;Port&nbsp;here</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;btnComOpen_Click(System.Object&nbsp;sender,&nbsp;System.EventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;device&nbsp;params</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var&nbsp;_with1&nbsp;=&nbsp;SerialPort1;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.ParityReplace&nbsp;=&nbsp;0x3b;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;replace&nbsp;&quot;;&quot;&nbsp;when&nbsp;parity&nbsp;error&nbsp;occurs</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.PortName&nbsp;=&nbsp;cboComPort.Text;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.BaudRate&nbsp;=&nbsp;Convert.ToInt32(cboBaudRate.Text);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.Parity&nbsp;=&nbsp;System.IO.Ports.Parity.None;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.DataBits&nbsp;=&nbsp;<span class="cs__number">8</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.StopBits&nbsp;=&nbsp;System.IO.Ports.StopBits.One;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.Handshake&nbsp;=&nbsp;System.IO.Ports.Handshake.None;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.RtsEnable&nbsp;=&nbsp;<span class="cs__keyword">false</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.ReceivedBytesThreshold&nbsp;=&nbsp;<span class="cs__number">1</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//threshold:&nbsp;one&nbsp;byte&nbsp;in&nbsp;buffer&nbsp;&gt;&nbsp;event&nbsp;is&nbsp;fired</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.NewLine&nbsp;=&nbsp;Constants.vbCr;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;CR&nbsp;must&nbsp;be&nbsp;the&nbsp;last&nbsp;char&nbsp;in&nbsp;frame.&nbsp;This&nbsp;terminates&nbsp;the&nbsp;SerialPort.readLine</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;_with1.ReadTimeout&nbsp;=&nbsp;<span class="cs__number">10000</span>;&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;check&nbsp;whether&nbsp;device&nbsp;is&nbsp;avaiable:</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">try</span>&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.Open();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;comOpen&nbsp;=&nbsp;SerialPort1.IsOpen;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span class="cs__keyword">catch</span>&nbsp;(Exception&nbsp;ex)&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;comOpen&nbsp;=&nbsp;<span class="cs__keyword">false</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Interaction.MsgBox(<span class="cs__string">&quot;Error&nbsp;Open:&nbsp;&quot;</span>&nbsp;&#43;&nbsp;ex.Message);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;picOpen.BackColor&nbsp;=&nbsp;Color.Red;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(comOpen)&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;picOpen.BackColor&nbsp;=&nbsp;Color.Green;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cboComPort.Enabled&nbsp;=&nbsp;<span class="cs__keyword">false</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cboBaudRate.Enabled&nbsp;=&nbsp;<span class="cs__keyword">false</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;close&nbsp;ComPort</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Button_Close_Click(System.Object&nbsp;sender,&nbsp;System.EventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(comOpen)&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;clear&nbsp;input&nbsp;buffer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.DiscardInBuffer();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.Close();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;comOpen&nbsp;=&nbsp;<span class="cs__keyword">false</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;picOpen.BackColor&nbsp;=&nbsp;Color.Red;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;picDataReceived.BackColor&nbsp;=&nbsp;Color.Gray;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cboComPort.Enabled&nbsp;=&nbsp;<span class="cs__keyword">true</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cboBaudRate.Enabled&nbsp;=&nbsp;<span class="cs__keyword">true</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;clear&nbsp;TextBoxes</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Button_clear_Click(System.Object&nbsp;sender,&nbsp;System.EventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tbRx.Text&nbsp;=&nbsp;<span class="cs__keyword">string</span>.Empty;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tbTx.Text&nbsp;=&nbsp;<span class="cs__keyword">string</span>.Empty;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;write&nbsp;content&nbsp;of&nbsp;Textbox&nbsp;to&nbsp;Port</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;button_send_Click(System.Object&nbsp;sender,&nbsp;System.EventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(comOpen)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.WriteLine(tbTx.Text);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;close&nbsp;app</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Button_ende_Click(System.Object&nbsp;sender,&nbsp;System.EventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(comOpen)&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;clear&nbsp;input&nbsp;buffer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.DiscardInBuffer();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.Close();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;comOpen&nbsp;=&nbsp;<span class="cs__keyword">false</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.Close();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;send&nbsp;control&nbsp;panel&nbsp;key&nbsp;to&nbsp;com&nbsp;port</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;param&nbsp;name=&quot;sender&quot;&gt;return&nbsp;key&nbsp;name&lt;/param&gt;</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Tasten_Click(System.Object&nbsp;sender,&nbsp;System.EventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">string</span>&nbsp;key&nbsp;=&nbsp;((Button)sender).Text;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(comOpen)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SerialPort1.Write(key);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;Timer&nbsp;datareceived&nbsp;event</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Timer1_Tick(System.Object&nbsp;sender,&nbsp;System.EventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;picDataReceived.BackColor&nbsp;=&nbsp;Color.Gray;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Timer1.Enabled&nbsp;=&nbsp;<span class="cs__keyword">false</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}<span class="cs__preproc">&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;#endregion</span><span class="cs__preproc">&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;#region&nbsp;&quot;ComPort&nbsp;read&nbsp;data</span>&quot;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;async&nbsp;read&nbsp;on&nbsp;secondary&nbsp;thread</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;SerialPort1_DataReceived(System.Object&nbsp;sender,&nbsp;System.IO.Ports.SerialDataReceivedEventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(comOpen)&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">try</span>&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;byteEnd&nbsp;=&nbsp;SerialPort1.NewLine.ToCharArray;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;get&nbsp;number&nbsp;off&nbsp;bytes&nbsp;in&nbsp;buffer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bytenumber&nbsp;=&nbsp;SerialPort1.BytesToRead;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;read&nbsp;one&nbsp;byte&nbsp;from&nbsp;buffer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//ByteToRead&nbsp;=&nbsp;SerialPort1.ReadByte()</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;read&nbsp;one&nbsp;char&nbsp;from&nbsp;buffer</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//CharToRead&nbsp;=&nbsp;SerialPort1.ReadChar()</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;read&nbsp;until&nbsp;string&nbsp;&quot;90&quot;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//readBuffer1&nbsp;=&nbsp;SerialPort1.ReadTo(&quot;90&quot;)</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;read&nbsp;entire&nbsp;string&nbsp;until&nbsp;.Newline&nbsp;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;readBuffer&nbsp;=&nbsp;SerialPort1.ReadLine();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//data&nbsp;to&nbsp;UI&nbsp;thread</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.Invoke(<span class="cs__keyword">new</span>&nbsp;EventHandler(DoUpdate));&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;<span class="cs__keyword">catch</span>&nbsp;(Exception&nbsp;ex)&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Interaction.MsgBox(<span class="cs__string">&quot;read&nbsp;&quot;</span>&nbsp;&#43;&nbsp;ex.Message);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;update&nbsp;received&nbsp;string&nbsp;in&nbsp;UI</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">///&nbsp;&lt;remarks&gt;&lt;/remarks&gt;</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;DoUpdate(<span class="cs__keyword">object</span>&nbsp;sender,&nbsp;System.EventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;tbRx.Text&nbsp;=&nbsp;readBuffer;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;picDataReceived.BackColor&nbsp;=&nbsp;Color.Green;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Timer1.Enabled&nbsp;=&nbsp;<span class="cs__keyword">true</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;mainForm()&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Load&nbsp;&#43;=&nbsp;Form1_Load;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;FormClosed&nbsp;&#43;=&nbsp;Form1_FormClosed;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;}<span class="cs__preproc">&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;#endregion</span>&nbsp;
}</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<h1>Backup</h1>
<p><strong>Bugfix&nbsp;no comport on system 30.7.2012</strong></p>
<p>Don't use this line:&nbsp;&nbsp;<span class="visualBasic__keyword">If</span>&nbsp;Portnames&nbsp;<span class="visualBasic__keyword">Is</span>&nbsp;<span class="visualBasic__keyword">Nothing</span>&nbsp;<span class="visualBasic__keyword">Then</span>&nbsp;</p>
<p>Change to: If Portnames.Length = 0 then</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
</div>
<p style="padding-left:30px">&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p style="padding-left:30px">&nbsp;</p>
<p style="padding-left:30px">&nbsp;</p>
<p>&nbsp;</p>
<p style="padding-left:30px">&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="endscriptcode"></div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
