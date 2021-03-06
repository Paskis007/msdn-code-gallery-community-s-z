# TCP / IP Server Client Example Part 7 (Chat Application)
## Requires
- Visual Studio 2013
## License
- MS-LPL
## Technologies
- C#
- SQL Server
- ADO.NET Entity Framework
- File System
- Class Library
- ADO.NET
- User Interface
- Windows Forms
- Microsoft Azure
- Data Access
- SQL Azure
- threading
- custom controls
- .NET Framework
- Visual Basic .NET
- Visual Basic.NET
- Parallel Programming
- Library
- Windows UI
- Network
- C# Language
- Async
- WinForms
- HttpClient
- Visual C Sharp .NET
- Windows Azure SQL Database
- .NET 4.5
- .NET Development
## Topics
- Controls
- C#
- Asynchronous Programming
- Security
- SQL Server
- Authentication
- Azure
- File System
- User Controls
- Class Library
- User Interface
- Windows Forms
- Globalization and Localization
- Multithreading
- Microsoft Azure
- Data Access
- threading
- events
- customization
- custom controls
- UI Layout
- Visual Basic .NET
- Logging
- Search
- VB.Net
- Parallel Programming
- Code Sample
- Getting Started
- Globalization
- Async
- Event Handling
- Messaging
- Notifications
- How to
- UI Design
- Generic C# resuable code
- Contacts
- File Systems
- Networking
- Storage
- HTTP
- Windows Forms Controls
- C# Language Features
- Language Samples
- User Control
- User Experience
- BitmapImage
- data and storage
## Updated
- 01/24/2014
## Description

<div>
<h1>1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Introduction</h1>
</div>
<p>Now we have our User&rsquo;s being saved to our Azure database we can add friends. In this chapter of the series that is exactly what we will be doing!</p>
<div>
<h1>2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Building the Sample</h1>
</div>
<p>The sample is built in Visual Studio 2013 Ultimate as an x86 targeted application using .Net Framework 4. We will be using NuGet packages, a number of 3rd party libraries, as well as Windows Azure. All of which will be fully explained to you ensuring that
 the final compilation of your App will be hassle free. Oh! And the sample code is verbosely commented so you should have no problem in working out what the code does.</p>
<p style="text-align:center"><strong>If you want me to continue writing this series please vote and if you feel like it why not recommend me for an MVP award here:
<a href="http://mvp.microsoft.com/en-us/nominate-an-mvp.aspx">http://mvp.microsoft.com/en-us/nominate-an-mvp.aspx</a></strong></p>
<div>
<h1>3&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Description</h1>
</div>
<p>If there is one thing a chat application needs more than any other feature is the ability of the users to find each other. In this incarnation of our application we allow our users to add their friends email address to their friends list. If the friend is
 registered with the chat server as well then the EU and their friend will be linked together as friends so that they can communicate. If on the other hand the friend is not registered the end user is told this.</p>
<p>We have done a refactor of the code and redesigned the Server, we have also split the Chat client out to a separate project. We have also added a Change Log (changes.txt) which tells us what we have done as we progress through the program also it allows
 us to add bugs that we have found during our testing.</p>
<h2>3.1&nbsp;&nbsp;&nbsp; Current Change Log:</h2>
<p>1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 24th of January 2014</p>
<p>2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; By Dave Gordon &lt;davesama@hotmail.co.uk&gt;</p>
<p>3&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Alpha Release For MSDN License: MS-PL</p>
<p>4&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Client&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Added Constants for the Command</p>
<p>5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Client&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Add Resources for the output
 - can be localized later</p>
<p>6&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Bug #3&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Server Does not close down properly - needs
 to be killed in TaskManager.</p>
<p>7&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Client&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Refactored &amp; Tidied the
 code into Regions</p>
<p>8&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Client&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Added the ability to Add Friends
 - and Prevented User from adding themselves as a friend</p>
<p>9&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Server&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Added the ability for friends to be added</p>
<p>10&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Server&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Added Command Not Implemented Yet</p>
<p>11&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AzureSQL&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Added Add Friend</p>
<p>12&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AzureSQL&nbsp;&nbsp; &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Added ClientIsLoggedIn</p>
<p>13&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Server&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Added a Close Down button - Needs Validation before close
 down</p>
<p>14&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 23rd of January 2014</p>
<p>15&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; By Dave Gordon &lt;davesama@hotmail.co.uk&gt;</p>
<p>16&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Alpha Release For MSDN License: MS-PL</p>
<p>17&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Added&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : This Document</p>
<p>18&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Added&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : NetComm Source so we can do changes to it later.</p>
<p>19&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Changed&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Startup application to Server (Allows us to run multiple Clients)</p>
<p>20&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Client&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Disabled Add Friend button until logged in</p>
<p>21&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Client&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Changed NetComm Reference to the included NetComm
 Code</p>
<p>22&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Client&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Recognizes Logged on Message from Server</p>
<p>23&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Server&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Changed NetComm Reference to the included NetComm Code</p>
<p>24&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; BUG #1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : After Registering Client needs to manually close and then login</p>
<p>25&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; BUG #2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; : Total Counters on Server not calculating correctly</p>
<p>&nbsp;</p>
<p>Remember when you start the server you will need to open the correct ports on your firewall, Windows will warn you with this dialog:</p>
<p>&nbsp;<img id="107773" src="107773-picture%202014-01-23%2004_05_46.png" alt="" width="539" height="388"></p>
<p>Click Allow access. If you do not have a firewall running, then start it immediately, and make sure your anti-virus is up to date. Microsoft supply a free Firewall and Anti-virus application with all modern Windows versions they release.</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div>
<h1>4&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Adding Friends</h1>
</div>
<p><img id="107774" src="107774-picture%202014-01-25%2002_26_11.png" alt="" width="362" height="149" style="float:left">We created a very simple form for adding friends which simply lets you add an email address. The form checks to make
 sure you did not add your own email address before sending the request to the server. The actual process is as follows:</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Check to see if the Email is registered</p>
<p>2&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; If they do exist attempt to add them as a friend</p>
<p>3&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; If that is successful tell the client the friend is added</p>
<p>4&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; The client tells the EU that the friend has been added</p>
<p>5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; If the friend does not exist we tell the client</p>
<p>6&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; The client tells the EU that the friend does not exist</p>
<p>The Add friend code looks like this:</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>

<div class="preview">
<pre class="csharp"><span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;DoAddFriend(<span class="cs__keyword">string</span>&nbsp;Sender,&nbsp;<span class="cs__keyword">string</span>&nbsp;message)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Awww&nbsp;they&nbsp;have&nbsp;a&nbsp;friend,&nbsp;that's&nbsp;nice</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;See&nbsp;if&nbsp;the&nbsp;Friend&nbsp;exists!</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(DoesUserEmailExist(Sender,&nbsp;message)&nbsp;&gt;&nbsp;<span class="cs__number">0</span>)&nbsp;<span class="cs__com">//&nbsp;If&nbsp;we&nbsp;get&nbsp;an&nbsp;ID&nbsp;then&nbsp;the&nbsp;user&nbsp;exists</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SendFriendAdded(Sender,&nbsp;message);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Add&nbsp;Friend&nbsp;to&nbsp;the&nbsp;database</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>&nbsp;(AzureDB.AddFriend(Sender,&nbsp;message.Split(<span class="cs__string">':'</span>)[<span class="cs__number">1</span>].ToString()))&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log(Resources.FriendWasSuccessfullyAdded);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Log(Resources.ErrorFriendWasNotAddedSuccessfully);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SendNoSuchUser(Sender,&nbsp;message);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>DoesUserEmailExist runs the following AzureDB command found in AzureSQL</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>SQL</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">mysql</span>

<div class="preview">
<pre class="mysql"><span class="sql__id">internal</span>&nbsp;<span class="sql__keyword">int</span>&nbsp;<span class="sql__id">GetUsersID</span>(<span class="sql__keyword">string</span>&nbsp;<span class="sql__id">emailAddress</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">int</span>&nbsp;<span class="sql__id">userID</span>&nbsp;=&nbsp;<span class="sql__number">0</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">string</span>&nbsp;<span class="sql__id">paramValue</span>&nbsp;=&nbsp;<span class="sql__id">emailAddress</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">string</span>&nbsp;<span class="sql__id">queryString</span>&nbsp;=&nbsp;<span class="sql__string">&quot;SELECT&nbsp;ClientID&nbsp;FROM&nbsp;dbo.Users&nbsp;WHERE&nbsp;EmailAddress&nbsp;=&nbsp;@emailAddress;&quot;</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">SqlCommand</span>&nbsp;<span class="sql__id">command</span>&nbsp;=&nbsp;<span class="sql__keyword">new</span>&nbsp;<span class="sql__id">SqlCommand</span>(<span class="sql__id">queryString</span>,&nbsp;<span class="sql__id">conn</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">command</span>.<span class="sql__id">Parameters</span>.<span class="sql__id">AddWithValue</span>(<span class="sql__string">&quot;@emailAddress&quot;</span>,&nbsp;<span class="sql__id">paramValue</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">userID</span>&nbsp;=&nbsp;(<span class="sql__keyword">int</span>)<span class="sql__id">command</span>.<span class="sql__id">ExecuteScalar</span>();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">return</span>&nbsp;<span class="sql__id">userID</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">catch</span>&nbsp;(<span class="sql__id">Exception</span>&nbsp;<span class="sql__id">ex</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">SQLInfoMessage</span>(<span class="sql__string">&quot;Error&nbsp;GetUsersID&nbsp;&quot;</span>&nbsp;&#43;&nbsp;<span class="sql__id">ex</span>.<span class="sql__id">Message</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">return</span>&nbsp;-<span class="sql__number">1</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</pre>
</div>
</div>
</div>
<div class="endscriptcode">&nbsp;</div>
<p>If the user gets any number above 0 (zero) then we know we have a valid user. The User&rsquo;s ID is returned. We then Add the friend to the EU&rsquo;s list of friends with the following AzureSQL command:</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>SQL</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Edit</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">mysql</span>

<div class="preview">
<pre class="mysql"><span class="sql__id">internal</span>&nbsp;<span class="sql__keyword">bool</span>&nbsp;<span class="sql__id">AddFriend</span>(<span class="sql__keyword">string</span>&nbsp;<span class="sql__id">Sender</span>,&nbsp;<span class="sql__keyword">string</span>&nbsp;<span class="sql__id">friendsEmail</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">try</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">int</span>&nbsp;<span class="sql__id">FriendsID</span>&nbsp;=&nbsp;<span class="sql__id">GetUsersID</span>(<span class="sql__id">friendsEmail</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">int</span>&nbsp;<span class="sql__id">SendersId</span>&nbsp;=&nbsp;<span class="sql__keyword">int</span>.<span class="sql__id">Parse</span>(<span class="sql__id">Sender</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">string</span>&nbsp;<span class="sql__id">queryString</span>&nbsp;=&nbsp;<span class="sql__string">&quot;INSERT&nbsp;INTO&nbsp;dbo.Friends&nbsp;(UserID,&nbsp;FriendsUserID)&nbsp;Values&nbsp;(@SendersId,&nbsp;@FriendsID);&quot;</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">SqlCommand</span>&nbsp;<span class="sql__id">command</span>&nbsp;=&nbsp;<span class="sql__keyword">new</span>&nbsp;<span class="sql__id">SqlCommand</span>(<span class="sql__id">queryString</span>,&nbsp;<span class="sql__id">conn</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">command</span>.<span class="sql__id">Parameters</span>.<span class="sql__id">AddWithValue</span>(<span class="sql__string">&quot;@SendersId&quot;</span>,&nbsp;<span class="sql__id">SendersId</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">command</span>.<span class="sql__id">Parameters</span>.<span class="sql__id">AddWithValue</span>(<span class="sql__string">&quot;@FriendsID&quot;</span>,&nbsp;<span class="sql__id">FriendsID</span>);&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">int</span>&nbsp;<span class="sql__id">RowsAffected</span>&nbsp;=&nbsp;(<span class="sql__keyword">int</span>)<span class="sql__id">command</span>.<span class="sql__id">ExecuteNonQuery</span>();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">if</span>&nbsp;(<span class="sql__id">RowsAffected</span>&nbsp;&gt;&nbsp;<span class="sql__number">0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">return</span>&nbsp;<span class="sql__value">true</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">return</span>&nbsp;<span class="sql__value">false</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">catch</span>&nbsp;(<span class="sql__id">Exception</span>&nbsp;<span class="sql__id">ex</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__id">SQLInfoMessage</span>(<span class="sql__string">&quot;Error&nbsp;RegisterUser&nbsp;&quot;</span>&nbsp;&#43;&nbsp;<span class="sql__id">ex</span>.<span class="sql__id">Message</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="sql__keyword">return</span>&nbsp;<span class="sql__value">false</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}</pre>
</div>
</div>
</div>
<h2>4.1&nbsp;&nbsp;&nbsp; To do:</h2>
<p>We now need to send the User&rsquo;s friends list back to the Client and have the client show those friends and their online status to the EU so that they can see who is available to chat to; that will be done in the next episode!</p>
<h2>4.2&nbsp;&nbsp;&nbsp; Source Code</h2>
<p>Solution</p>
<ul>
<li>Changes.Txt &ndash; Kept updated with each change made to the code, and with any bugs found during testing
</li></ul>
<p>ChatClient</p>
<ul>
<li>FrmChat.cs &ndash; The Main Chat Client program </li><li>FrmLogin.cs &ndash; The Login form for the End User </li><li>FrmRegister.cs &ndash; The Registration form for the End User, so they do not have to go to a website to register.
</li></ul>
<p>ServerClientChat</p>
<ul>
<li>FrmServer.cs &ndash; The Main Server Application </li><li>FrmAzureDatabaseLogin.cs &ndash; Login Form for your Azure Database </li><li>Classes/AzureSQL.cs &ndash; This contains all our SQL connection and queries for our database
</li><li>Classes/PublicIP.cs &ndash; This is used to obtain our public IP address </li></ul>
<p>NetComm</p>
<ul>
<li>Functions.vb </li><li>NetComm.vb </li></ul>
<p>Configuration Files</p>
<ul>
<li>In MyDocuments/ChatAzureDB.txt &ndash; This contains the login details for the Azure Database.
</li></ul>
<div>
<h1>5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; More Information</h1>
<ul>
<li>To convert the solution to a previous version of Visual Studio you can use this free application:
<a href="http://vsprojectconverter.codeplex.com/">http://vsprojectconverter.codeplex.com/</a> or download and use Visual Studio 2013 Express which is freely available from Microsoft from here:
<a href="http://www.visualstudio.com/downloads/download-visual-studio-vs">http://www.visualstudio.com/downloads/download-visual-studio-vs</a>.
</li><li>NetComm.dll: <a href="http://www.codeproject.com/Articles/118485/C-VB-NET-Multi-user-Communication-Library-TCP">
http://www.codeproject.com/Articles/118485/C-VB-NET-Multi-user-Communication-Library-TCP</a>
</li><li>The Visual Basic version of this code was generated by the tool: Instant VB from
<a href="http://www.tangiblesoftwaresolutions.com/">http://www.tangiblesoftwaresolutions.com/</a> - There is a free version available as well!
</li><li>Microsoft Firewall: <a href="http://windows.microsoft.com/en-gb/windows/turn-windows-firewall-on-off#turn-windows-firewall-on-off=windows-vista">
http://windows.microsoft.com/en-gb/windows/turn-windows-firewall-on-off#turn-windows-firewall-on-off=windows-vista</a>
</li><li>Microsoft Anti-Virus: <a href="http://www.pcadvisor.co.uk/how-to/windows/3466684/how-turn-on-defender-in-windows-8/">
http://www.pcadvisor.co.uk/how-to/windows/3466684/how-turn-on-defender-in-windows-8/</a>
</li><li>Microsoft MVP &ndash; Nominate Me Please: <a href="http://mvp.microsoft.com/en-us/nominate-an-mvp.aspx">
http://mvp.microsoft.com/en-us/nominate-an-mvp.aspx</a> </li></ul>
</div>
