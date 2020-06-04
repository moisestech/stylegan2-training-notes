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
<li>Use <a href="https://pypi.org/project/gdown/">GDown</a></li>
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
<li>
<p>Change --dataset=””</p>
</li>
<li>
<p>By ignoring vertical = false</p>
</li>
<li>
<p>Total kimages 20k is fine</p>
</li>
<li>
<p>—res-log2=7 power of 2</p>
</li>
<li>
<p>w=2^6  768</p>
</li>
<li>
<p>h=2^8*5  1200</p>
</li>
<li>
<p>Image sizes 128 or 256s</p>
</li>
<li>
<p>This repo recommends that if you are doing 128 it recommends you use 7</p>
</li>
<li>
<p>Because that 8th channel although it makes the network a little bit deeper it makes it smaller overall</p>
</li>
<li>
<p>You can’t do a 16:9 or 720p</p>
</li>
</ul>
<h2 id="start-training">Start Training</h2>
<ul>
<li>We are ready to start training this picks up from this pkl file</li>
<li>Covert some things its a bit slower the first time because it is caching some files</li>
<li>Data shape, dynamic shape</li>
<li>Range 0-255 256 the size that we can work with loading networks</li>
<li>Custom Cuda commands compile</li>
<li>(2- 5 minute wait)</li>
<li>Outputting the architecture</li>
<li>Note hub mode works</li>
<li>Building Tensorflow graph</li>
<li>Training for 20k images</li>
<li>In csse your dataset the tfrecorsd creation and thow an error here</li>
<li>You will produce a pkl file from its current status</li>
<li>Gcp close when i close</li>
<li>Outputting pickling up from the same imag</li>
<li>Large of the mini batches</li>
<li>Timing how much memory im using underestimates</li>
<li>Ctrl C</li>
<li>The issue was reactivate the right environment</li>
<li>Run this script</li>
<li>Nohup close this browser window it would stop that command</li>
<li>You could install gnu you could installl gmux</li>
<li>Nohup ,out asses wether this is working</li>
<li>5 mins after</li>
<li>Background in nohup</li>
<li>Essentially it is a background process on the gpu</li>
<li>Nvdia -smi</li>
<li>Cuda version 4.0</li>
<li>How much gpu are you using</li>
<li>Process ID python 15.7gb</li>
<li>This is your command running on the gpu</li>
<li>Kill -9 PID number</li>
</ul>
<h2 id="day-of-training-later..">1 Day of Training Later…</h2>
<ul>
<li>24 hours of training later</li>
<li>Skyfly nil folder</li>
<li>Nvdia smi</li>
</ul>
<p><code>ls results</code><br>
<code>cd/results/0003-stylegan2-your_dataset_name</code></p>
<ul>
<li>80k images later the flower are swirly 500k images gets to a really good point</li>
<li>Truncation value good looking stuff</li>
<li>Download the nohup .out file<br>
<code>ls pwd</code></li>
<li>Download file no-hub.out</li>
<li>Scroll to the bottom</li>
<li>Text output</li>
<li>A tick is a certain number of kimages what you set a mini batch too</li>
<li>How long does it take to train a tick faster with how quickly it takes</li>
</ul>

