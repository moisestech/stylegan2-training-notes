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

