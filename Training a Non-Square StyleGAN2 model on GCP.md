---


---

<h1 id="training-a-non-square-stylegan2-model-on-gcp">Training a Non-Square StyleGAN2 model on GCP</h1>
<p><strong>#stylegan2</strong> <strong>#non-square</strong>  <strong>#gcp</strong></p>
<p>Notes 📝 based on <a href="www.youtube.com/watch?v=Ij1dqSVR89M">Training StyleGAN2 Part 2 Video</a> 🎥 taught in the <a href="%5Bhttps://bustbright.square.site/s/shop%5D(https://bustbright.square.site/s/shop)">StyleGAN2 DeepDive course</a> 📚by <a href="%5Bhttps://twitter.com/dvsch%5D(https://twitter.com/dvsch)">@Derrick Schultz</a> and <a href="%5Bhttps://twitter.com/Lialialiacole%5D(https://twitter.com/Lialialiacole)">@Lia Coleman</a>.</p>
<h2 id="start-up-server-gear">1. Start-up Server ⚙️</h2>
<ol>
<li>Login into <a href="console.cloud.google.com">GCP</a></li>
<li>Click launch on your Compute account. (image?)</li>
</ol>
<p><strong>Notes:</strong></p>
<ul>
<li>Have your dataset ready and uploaded in 📁Google Drive.
<ul>
<li>Vertical 🎨 Images: 767px by 1200px</li>
<li>Square 🎨 Images: 1024px by 1024px</li>
</ul>
</li>
<li>Refer to the Github :octocat: repo <a href="https://github.com/skyflynil/stylegan2">skyfkynil/stylegan2</a>  for detailed directions.</li>
<li>For further information refer to the paper Official TensorFlow Implementation with practical improvements 📄<a href="http://arxiv.org/abs/1912.04958">http://arxiv.org/abs/1912.04958</a></li>
</ul>
<h2 id="ssh-login-open-in-browser-window-computer">2. SSH Login Open in Browser Window 💻</h2>
<ul>
<li>Click Login through SSH. (image?)
<ul>
<li>Out of the box doesn’t have static IP (It can be set-up)</li>
</ul>
</li>
</ul>
<h2 id="activate-stylegan2-library-snake">3. Activate StyleGAN2 library 🐍</h2>
<ol>
<li>In Terminal activate your anaconda environment.<pre><code>conda activate stylegan
</code></pre>
</li>
</ol>
<h2 id="set-up-dataset-folder-file_folder">4.  Set-up Dataset Folder 📁</h2>
<ol>
<li>Move into the skyflynil folder and go into the folder <em>datasets</em></li>
<li>Place all tfrecords in the datasets folder.</li>
<li>Create raw_datasets folder<pre><code>mkdir raw_datasets
</code></pre>
<ul>
<li>(Why? To differentiate raw images from tfrecord folders)</li>
</ul>
</li>
<li>Go inside your new folder<pre><code>cd into raw_datasets
</code></pre>
</li>
</ol>
<h2 id="upload-dataset-images-in-gcp-arrow_up">5. Upload Dataset images in GCP ⬆️</h2>
<ol>
<li>Use GDown</li>
<li>Pass the ID to a file</li>
<li>On GDrive, toggle Share linking on and copy the ID<pre><code>gdown --id id-ofyour-gdrive-zip-file
</code></pre>
<ul>
<li>GServer to GServer is really fast</li>
</ul>
</li>
</ol>
<h2 id="unzip">6. Unzip</h2>
<ol>
<li>Unzip your gdown file<pre><code>unzip dataset-name.zip
</code></pre>
</li>
<li>Clean up your raw_dataset folder by removing the zip file</li>
</ol>
<pre><code>rm dataset-name.zip 
</code></pre>
<ol start="3">
<li>Go back to the main styleGAN2 folder<pre><code>..//
</code></pre>
</li>
</ol>
<h2 id="create-our-tfrecords-files">7. Create our tfrecords files</h2>
<ol>
<li>Create tfrecords from your image files, rather than training from raw-images (optimization)<pre><code>!python dataset_tool.py create_from_images_raw --res_log2=8 ./dataset/dataset_name ./raw_datasets/dataset-name/
</code></pre>
<ul>
<li>you should see raw-dataset tfrecords file</li>
<li>(base) stylegan-ver: 1</li>
</ul>
</li>
</ol>
<p>python dataset_tool.py create_from_images_raw dataset_dir raw_image_dir<br>
<strong>Notes</strong></p>
<ul>
<li>
<p>For information on installing your anaconda environment check out the video <a href="%5Bhttps://www.youtube.com/watch?v=59hpiFMjhpY%5D(https://www.youtube.com/watch?v=59hpiFMjhpY)">StyleGAN2 installation on GCP</a> 🎥</p>
</li>
<li>
<p>Documentation link to <a href="%5Bhttps://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#viewing-a-list-of-your-environments%5D(https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#viewing-a-list-of-your-environments)">listing out your anaconda environments</a> on Terminal</p>
</li>
<li>
<p>Config e 512</p>
</li>
<li>
<p>Config f 1024</p>
</li>
</ul>
<p>Change --dataset=””</p>
<p>By ignoring vertical = false</p>
<p>Total kimages 20k is fine</p>
<p>–res-log2=7 power of 2</p>
<p>w=2^6  768</p>
<p>h=2^8*5  1200</p>
<p>Image sizes 128 or 256s</p>
<p>This repo recommends that if you are doing 128 it recommends you use 7</p>
<p>Because that 8th channel although it makes the network a little bit deeper it makes it smaller overall</p>
<p>You can’t do a 16:9 or 720p</p>
<p>We are ready to start training this picks up from this pkl file</p>
<p>Covert some things its a bit slower the first time because it is caching some files</p>
<p>Data shape, dynamic shape</p>
<p>Range 0-255 256 the size that we can work with loading networks</p>
<p>Custom Cuda commands compile</p>
<p>(2- 5 minute wait)</p>
<p>Outputting the architecture</p>
<p>Note hub mode works</p>
<p>Building Tensorflow graph</p>
<p>Training for 20k im,ages</p>
<p>In csse your dataset the tfrecorsd creation and thow an error here</p>
<p>You will produce a pkl file from its current status</p>
<p>Gcp close when i close</p>
<p>Outputting pickling up from the same imag</p>
<p>Large of the minibatches</p>
<p>Timing how much memory im using underestimates</p>
<p>Ctrl C</p>
<p>The issue was reactivate the right environment</p>
<p>Run this script</p>
<p>Nohup close this browser window it would stop that command</p>
<p>You could install gnu you could installl gmux</p>
<p>Nohup ,out asses wether this is working</p>
<ul>
<li>
<p>5 mins after</p>
</li>
<li>
<p>Background in nohup</p>
</li>
<li>
<p>Essentially it is a background process on the gpu</p>
</li>
<li>
<p>Nvdia -smi</p>
</li>
<li>
<p>Cuda version 4.0</p>
</li>
<li>
<p>How much gpu are you using</p>
</li>
</ul>
<p>Process ID python 15.7gb</p>
<ul>
<li>
<p>This is your command running on the gpu</p>
</li>
<li>
<p>Kill -9 PID number</p>
</li>
</ul>
<p>24 hours</p>
<ul>
<li>
<p>Skyfly nil folder</p>
</li>
<li>
<p>Nvdia smi</p>
</li>
<li>
<p>Ls results</p>
</li>
<li>
<p>cd/results/0003-stylegan2-your_dataset_name</p>
</li>
<li>
<p>80k images later the flower are swirly 500k images gets to a really good point</p>
</li>
<li>
<p>Truncation value good looking stuff</p>
</li>
</ul>
<p>Download the nohup .out file</p>
<p>Ls pwd</p>
<p>Download file no-hub.out</p>
<p>Scroll to the bottom</p>
<p>Text output</p>
<p>A tick is a certain number of kimages what you set a mini batch too</p>
<p>How long does it take to train a tick faster with how quickly it takes</p>
<p>The file explorer is accessible using the button in left corner of the navigation bar. You can create a new file by clicking the <strong>New file</strong> button in the file explorer. You can also create folders by clicking the <strong>New folder</strong> button.</p>
<h2 id="switch-to-another-file">Switch to another file</h2>
<p>All your files and folders are presented as a tree in the file explorer. You can switch from one to another by clicking a file in the tree.</p>
<h2 id="rename-a-file">Rename a file</h2>
<p>You can rename the current file by clicking the file name in the navigation bar or by clicking the <strong>Rename</strong> button in the file explorer.</p>
<h2 id="delete-a-file">Delete a file</h2>
<p>You can delete the current file by clicking the <strong>Remove</strong> button in the file explorer. The file will be moved into the <strong>Trash</strong> folder and automatically deleted after 7 days of inactivity.</p>
<h2 id="export-a-file">Export a file</h2>
<p>You can export the current file by clicking <strong>Export to disk</strong> in the menu. You can choose to export the file as plain Markdown, as HTML using a Handlebars template or as a PDF.</p>
<h1 id="synchronization">Synchronization</h1>
<p>Synchronization is one of the biggest features of StackEdit. It enables you to synchronize any file in your workspace with other files stored in your <strong>Google Drive</strong>, your <strong>Dropbox</strong> and your <strong>GitHub</strong> accounts. This allows you to keep writing on other devices, collaborate with people you share the file with, integrate easily into your workflow… The synchronization mechanism takes place every minute in the background, downloading, merging, and uploading file modifications.</p>
<p>There are two types of synchronization and they can complement each other:</p>
<ul>
<li>
<p>The workspace synchronization will sync all your files, folders and settings automatically. This will allow you to fetch your workspace on any other device.</p>
<blockquote>
<p>To start syncing your workspace, just sign in with Google in the menu.</p>
</blockquote>
</li>
<li>
<p>The file synchronization will keep one file of the workspace synced with one or multiple files in <strong>Google Drive</strong>, <strong>Dropbox</strong> or <strong>GitHub</strong>.</p>
<blockquote>
<p>Before starting to sync files, you must link an account in the <strong>Synchronize</strong> sub-menu.</p>
</blockquote>
</li>
</ul>
<h2 id="open-a-file">Open a file</h2>
<p>You can open a file from <strong>Google Drive</strong>, <strong>Dropbox</strong> or <strong>GitHub</strong> by opening the <strong>Synchronize</strong> sub-menu and clicking <strong>Open from</strong>. Once opened in the workspace, any modification in the file will be automatically synced.</p>
<h2 id="save-a-file">Save a file</h2>
<p>You can save any file of the workspace to <strong>Google Drive</strong>, <strong>Dropbox</strong> or <strong>GitHub</strong> by opening the <strong>Synchronize</strong> sub-menu and clicking <strong>Save on</strong>. Even if a file in the workspace is already synced, you can save it to another location. StackEdit can sync one file with multiple locations and accounts.</p>
<h2 id="synchronize-a-file">Synchronize a file</h2>
<p>Once your file is linked to a synchronized location, StackEdit will periodically synchronize it by downloading/uploading any modification. A merge will be performed if necessary and conflicts will be resolved.</p>
<p>If you just have modified your file and you want to force syncing, click the <strong>Synchronize now</strong> button in the navigation bar.</p>
<blockquote>
<p><strong>Note:</strong> The <strong>Synchronize now</strong> button is disabled if you have no file to synchronize.</p>
</blockquote>
<h2 id="manage-file-synchronization">Manage file synchronization</h2>
<p>Since one file can be synced with multiple locations, you can list and manage synchronized locations by clicking <strong>File synchronization</strong> in the <strong>Synchronize</strong> sub-menu. This allows you to list and remove synchronized locations that are linked to your file.</p>
<h1 id="publication">Publication</h1>
<p>Publishing in StackEdit makes it simple for you to publish online your files. Once you’re happy with a file, you can publish it to different hosting platforms like <strong>Blogger</strong>, <strong>Dropbox</strong>, <strong>Gist</strong>, <strong>GitHub</strong>, <strong>Google Drive</strong>, <strong>WordPress</strong> and <strong>Zendesk</strong>. With <a href="http://handlebarsjs.com/">Handlebars templates</a>, you have full control over what you export.</p>
<blockquote>
<p>Before starting to publish, you must link an account in the <strong>Publish</strong> sub-menu.</p>
</blockquote>
<h2 id="publish-a-file">Publish a File</h2>
<p>You can publish your file by opening the <strong>Publish</strong> sub-menu and by clicking <strong>Publish to</strong>. For some locations, you can choose between the following formats:</p>
<ul>
<li>Markdown: publish the Markdown text on a website that can interpret it (<strong>GitHub</strong> for instance),</li>
<li>HTML: publish the file converted to HTML via a Handlebars template (on a blog for example).</li>
</ul>
<h2 id="update-a-publication">Update a publication</h2>
<p>After publishing, StackEdit keeps your file linked to that publication which makes it easy for you to re-publish it. Once you have modified your file and you want to update your publication, click on the <strong>Publish now</strong> button in the navigation bar.</p>
<blockquote>
<p><strong>Note:</strong> The <strong>Publish now</strong> button is disabled if your file has not been published yet.</p>
</blockquote>
<h2 id="manage-file-publication">Manage file publication</h2>
<p>Since one file can be published to multiple locations, you can list and manage publish locations by clicking <strong>File publication</strong> in the <strong>Publish</strong> sub-menu. This allows you to list and remove publication locations that are linked to your file.</p>
<h1 id="markdown-extensions">Markdown extensions</h1>
<p>StackEdit extends the standard Markdown syntax by adding extra <strong>Markdown extensions</strong>, providing you with some nice features.</p>
<blockquote>
<p><strong>ProTip:</strong> You can disable any <strong>Markdown extension</strong> in the <strong>File properties</strong> dialog.</p>
</blockquote>
<h2 id="smartypants">SmartyPants</h2>
<p>SmartyPants converts ASCII punctuation characters into “smart” typographic punctuation HTML entities. For example:</p>

<table>
<thead>
<tr>
<th></th>
<th>ASCII</th>
<th>HTML</th>
</tr>
</thead>
<tbody>
<tr>
<td>Single backticks</td>
<td><code>'Isn't this fun?'</code></td>
<td>‘Isn’t this fun?’</td>
</tr>
<tr>
<td>Quotes</td>
<td><code>"Isn't this fun?"</code></td>
<td>“Isn’t this fun?”</td>
</tr>
<tr>
<td>Dashes</td>
<td><code>-- is en-dash, --- is em-dash</code></td>
<td>– is en-dash, — is em-dash</td>
</tr>
</tbody>
</table><h2 id="katex">KaTeX</h2>
<p>You can render LaTeX mathematical expressions using <a href="https://khan.github.io/KaTeX/">KaTeX</a>:</p>
<p>The <em>Gamma function</em> satisfying <span class="katex--inline"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi mathvariant="normal">Γ</mi><mo stretchy="false">(</mo><mi>n</mi><mo stretchy="false">)</mo><mo>=</mo><mo stretchy="false">(</mo><mi>n</mi><mo>−</mo><mn>1</mn><mo stretchy="false">)</mo><mo stretchy="false">!</mo><mspace width="1em"></mspace><mi mathvariant="normal">∀</mi><mi>n</mi><mo>∈</mo><mi mathvariant="double-struck">N</mi></mrow><annotation encoding="application/x-tex">\Gamma(n) = (n-1)!\quad\forall n\in\mathbb N</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord">Γ</span><span class="mopen">(</span><span class="mord mathdefault">n</span><span class="mclose">)</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mopen">(</span><span class="mord mathdefault">n</span><span class="mspace" style="margin-right: 0.222222em;"></span><span class="mbin">−</span><span class="mspace" style="margin-right: 0.222222em;"></span></span><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord">1</span><span class="mclose">)</span><span class="mclose">!</span><span class="mspace" style="margin-right: 1em;"></span><span class="mord">∀</span><span class="mord mathdefault">n</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">∈</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 0.68889em; vertical-align: 0em;"></span><span class="mord mathbb">N</span></span></span></span></span> is via the Euler integral</p>
<p><span class="katex--display"><span class="katex-display"><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mi mathvariant="normal">Γ</mi><mo stretchy="false">(</mo><mi>z</mi><mo stretchy="false">)</mo><mo>=</mo><msubsup><mo>∫</mo><mn>0</mn><mi mathvariant="normal">∞</mi></msubsup><msup><mi>t</mi><mrow><mi>z</mi><mo>−</mo><mn>1</mn></mrow></msup><msup><mi>e</mi><mrow><mo>−</mo><mi>t</mi></mrow></msup><mi>d</mi><mi>t</mi> <mi mathvariant="normal">.</mi></mrow><annotation encoding="application/x-tex">
\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.
</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord">Γ</span><span class="mopen">(</span><span class="mord mathdefault" style="margin-right: 0.04398em;">z</span><span class="mclose">)</span><span class="mspace" style="margin-right: 0.277778em;"></span><span class="mrel">=</span><span class="mspace" style="margin-right: 0.277778em;"></span></span><span class="base"><span class="strut" style="height: 2.32624em; vertical-align: -0.91195em;"></span><span class="mop"><span class="mop op-symbol large-op" style="margin-right: 0.44445em; position: relative; top: -0.001125em;">∫</span><span class="msupsub"><span class="vlist-t vlist-t2"><span class="vlist-r"><span class="vlist" style="height: 1.41429em;"><span class="" style="top: -1.78805em; margin-left: -0.44445em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight">0</span></span></span><span class="" style="top: -3.8129em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight">∞</span></span></span></span><span class="vlist-s">​</span></span><span class="vlist-r"><span class="vlist" style="height: 0.91195em;"><span class=""></span></span></span></span></span></span><span class="mspace" style="margin-right: 0.166667em;"></span><span class="mord"><span class="mord mathdefault">t</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.864108em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mathdefault mtight" style="margin-right: 0.04398em;">z</span><span class="mbin mtight">−</span><span class="mord mtight">1</span></span></span></span></span></span></span></span></span><span class="mord"><span class="mord mathdefault">e</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height: 0.843556em;"><span class="" style="top: -3.113em; margin-right: 0.05em;"><span class="pstrut" style="height: 2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight"><span class="mord mtight">−</span><span class="mord mathdefault mtight">t</span></span></span></span></span></span></span></span></span><span class="mord mathdefault">d</span><span class="mord mathdefault">t</span><span class="mspace" style="margin-right: 0.166667em;"></span><span class="mord">.</span></span></span></span></span></span></p>
<blockquote>
<p>You can find more information about <strong>LaTeX</strong> mathematical expressions <a href="http://meta.math.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference">here</a>.</p>
</blockquote>
<h2 id="uml-diagrams">UML diagrams</h2>
<p>You can render UML diagrams using <a href="https://mermaidjs.github.io/">Mermaid</a>. For example, this will produce a sequence diagram:</p>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-yUyQGR3LStVtgohI" height="100%" width="100%" style="max-width:750px;" viewBox="-50 -10 750 469"><g></g><g><line id="actor111" x1="75" y1="5" x2="75" y2="458" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="0" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="75" dy="0">Alice</tspan></text></g><g><line id="actor112" x1="275" y1="5" x2="275" y2="458" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="200" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="275" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="275" dy="0">Bob</tspan></text></g><g><line id="actor113" x1="475" y1="5" x2="475" y2="458" class="actor-line" stroke-width="0.5px" stroke="#999"></line><rect x="400" y="0" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="475" y="32.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="475" dy="0">John</tspan></text></g><defs><marker id="arrowhead" refX="5" refY="2" markerWidth="6" markerHeight="4" orient="auto"><path d="M 0,0 V 4 L6,2 Z"></path></marker></defs><defs><marker id="crosshead" markerWidth="15" markerHeight="8" orient="auto" refX="16" refY="4"><path fill="black" stroke="#000000" stroke-width="1px" d="M 9,2 V 6 L16,4 Z" style="stroke-dasharray: 0, 0;"></path><path fill="none" stroke="#000000" stroke-width="1px" d="M 0,1 L 6,7 M 6,1 L 0,7" style="stroke-dasharray: 0, 0;"></path></marker></defs><g><text x="175" y="93" class="messageText" style="text-anchor: middle;">Hello Bob, how are you?</text><line x1="75" y1="100" x2="275" y2="100" class="messageLine0" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="fill: none;"></line></g><g><text x="375" y="128" class="messageText" style="text-anchor: middle;">How about you John?</text><line x1="275" y1="135" x2="475" y2="135" class="messageLine1" stroke-width="2" stroke="black" marker-end="url(#arrowhead)" style="stroke-dasharray: 3, 3; fill: none;"></line></g><g><text x="175" y="163" class="messageText" style="text-anchor: middle;">I am good thanks!</text><line x1="275" y1="170" x2="75" y2="170" class="messageLine1" stroke-width="2" stroke="black" marker-end="url(#crosshead)" style="stroke-dasharray: 3, 3; fill: none;"></line></g><g><text x="375" y="198" class="messageText" style="text-anchor: middle;">I am good thanks!</text><line x1="275" y1="205" x2="475" y2="205" class="messageLine0" stroke-width="2" stroke="black" marker-end="url(#crosshead)" style="fill: none;"></line></g><g><rect x="500" y="215" fill="#EDF2AE" stroke="#666" width="150" height="88" rx="0" ry="0" class="note"></rect><text x="496" y="239" fill="black" class="noteText"><tspan x="516" fill="black">Bob thinks a long</tspan></text><text x="496" y="256" fill="black" class="noteText"><tspan x="516" fill="black">long time, so long</tspan></text><text x="496" y="273" fill="black" class="noteText"><tspan x="516" fill="black">that the text does</tspan></text><text x="496" y="290" fill="black" class="noteText"><tspan x="516" fill="black">not fit on a row.</tspan></text></g><g><text x="175" y="331" class="messageText" style="text-anchor: middle;">Checking with John...</text><line x1="275" y1="338" x2="75" y2="338" class="messageLine1" stroke-width="2" stroke="black" style="stroke-dasharray: 3, 3; fill: none;"></line></g><g><text x="275" y="366" class="messageText" style="text-anchor: middle;">Yes... John, how are you?</text><line x1="75" y1="373" x2="475" y2="373" class="messageLine0" stroke-width="2" stroke="black" style="fill: none;"></line></g><g><rect x="0" y="393" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="75" y="425.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="75" dy="0">Alice</tspan></text></g><g><rect x="200" y="393" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="275" y="425.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="275" dy="0">Bob</tspan></text></g><g><rect x="400" y="393" fill="#eaeaea" stroke="#666" width="150" height="65" rx="3" ry="3" class="actor"></rect><text x="475" y="425.5" dominant-baseline="central" alignment-baseline="central" class="actor" style="text-anchor: middle;"><tspan x="475" dy="0">John</tspan></text></g></svg></div>
<p>And this will produce a flow chart:</p>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-0RYlDy6JHNI6i6zB" width="100%" style="max-width: 500.3109359741211px;" viewBox="0 0 500.3109359741211 171.890625"><g transform="translate(-12, -12)"><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath" style="opacity: 1;"><path class="path" d="M119.91170576572816,78.41796875L179.3203125,49.9453125L255.2578125,49.9453125" marker-end="url(#arrowhead69)" style="fill:none"></path><defs><marker id="arrowhead69" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M119.91170576572816,124.41796875L179.3203125,152.890625L234.796875,152.890625" marker-end="url(#arrowhead70)" style="fill:none"></path><defs><marker id="arrowhead70" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M315.1484375,49.9453125L360.609375,49.9453125L408.6013871293077,79.42595738363185" marker-end="url(#arrowhead71)" style="fill:none"></path><defs><marker id="arrowhead71" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M335.609375,152.890625L360.609375,152.890625L408.6013861816871,124.4099806946266" marker-end="url(#arrowhead72)" style="fill:none"></path><defs><marker id="arrowhead72" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" transform="translate(179.3203125,49.9453125)" style="opacity: 1;"><g transform="translate(-30.4765625,-13)" class="label"><foreignObject width="60.953125" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel">Link text</span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g></g><g class="nodes"><g class="node" id="A" transform="translate(71.921875,101.41796875)" style="opacity: 1;"><rect rx="0" ry="0" x="-51.921875" y="-23" width="103.84375" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-41.921875,-13)"><foreignObject width="83.84375" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Square Rect</div></foreignObject></g></g></g><g class="node" id="B" transform="translate(285.203125,49.9453125)" style="opacity: 1;"><circle x="-29.9453125" y="-23" r="29.9453125"></circle><g class="label" transform="translate(0,0)"><g transform="translate(-19.9453125,-13)"><foreignObject width="39.890625" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Circle</div></foreignObject></g></g></g><g class="node" id="C" transform="translate(285.203125,152.890625)" style="opacity: 1;"><rect rx="5" ry="5" x="-50.40625" y="-23" width="100.8125" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-40.40625,-13)"><foreignObject width="80.8125" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Round Rect</div></foreignObject></g></g></g><g class="node" id="D" transform="translate(444.96015548706055,101.41796875)" style="opacity: 1;"><polygon points="59.350781250000004,0 118.70156250000001,-59.350781250000004 59.350781250000004,-118.70156250000001 0,-59.350781250000004" rx="5" ry="5" transform="translate(-59.350781250000004,59.350781250000004)"></polygon><g class="label" transform="translate(0,0)"><g transform="translate(-32.9453125,-13)"><foreignObject width="65.890625" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Rhombus</div></foreignObject></g></g></g></g></g></g></svg></div>

