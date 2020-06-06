---


---

<h1 id="training-a-non-square-stylegan2-model-on-gcp">Training a Non-Square StyleGAN2 model on GCP</h1>
<p><strong>#stylegan2</strong> <strong>#non-square</strong>  <strong>#gcp</strong></p>
<p>Notes 📝 based on <a href="www.youtube.com/watch?v=Ij1dqSVR89M">Training StyleGAN2 Part 2 Video</a> 🎥 taught in the <a href="%5Bhttps://bustbright.square.site/s/shop%5D(https://bustbright.square.site/s/shop)">StyleGAN2 DeepDive course</a> 📚by <a href="%5Bhttps://twitter.com/dvsch%5D(https://twitter.com/dvsch)">@Derrick Schultz</a> and <a href="%5Bhttps://twitter.com/Lialialiacole%5D(https://twitter.com/Lialialiacole)">@Lia Coleman</a>.</p>
<h2 id="start-up-server-gear-">1. Start-up Server ⚙️ *</h2>
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
<h2 id="ssh-login-open-in-browser-window-computer-">2. SSH Login Open in Browser Window 💻 *</h2>
<ul>
<li>Click Login through SSH. (image?)
<ul>
<li>Out of the box doesn’t have static IP (It can be set-up)</li>
</ul>
</li>
</ul>
<h2 id="activate-stylegan2-library-snake-">3. Activate StyleGAN2 library 🐍 *</h2>
<ol>
<li>In Terminal activate your anaconda environment.<pre><code>conda activate stylegan
</code></pre>
</li>
</ol>
<h2 id="set-up-dataset-folder-file_folder-">4.  Set-up Dataset Folder 📁 *</h2>
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
<h2 id="upload-dataset-images-in-gcp-arrow_up-">5. Upload Dataset images in GCP ⬆️ *</h2>
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
<h2 id="unzip-closed_lock_with_key-">6. Unzip 🔐 *</h2>
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
<h2 id="create-our-tfrecords-files-">7. Create our TFRecords files <a href="https://youtu.be/Ij1dqSVR89M?t=363">*</a></h2>
<ol>
<li>Create TFRecords from your image files, rather than training from raw-images (optimization)<pre><code>!python dataset_tool.py create_from_images_raw --res_log2=8 ./dataset/dataset_name ./raw_datasets/dataset-name/
</code></pre>
<ul>
<li>you should see raw-dataset TFRecords file</li>
<li>(base) stylegan-ver: 1</li>
</ul>
</li>
</ol>
<p><strong>Notes</strong></p>
<ul>
<li>
<p><strong>Detailed instruction for training your <a href="https://github.com/skyflynil/stylegan2">stylegan2 skyflynil notes</a></strong></p>
<ul>
<li>
<p>Instead of image size of 2^n * 2^n, now you can process your image size as of (min_h x 2^n) X (min_w * 2^n) naturally. For example, 640x384, min_h = 5, min_w =3, n=7. Please make sure all your raw images are preprocessed to the exact same size. To reduce the training set size, JPEG format is preferred.</p>
</li>
<li>
<p>For image size 1280x768 (hxw), you may choose (min_h, min_w, res_log2) as (10, 6, 7) or (5, 3, 8) , the latter setup is preferred due to deeper and smaller network, change res_log2 argument for dataset creation and training accordingly.</p>
</li>
</ul>
</li>
<li>
<p>For information on installing your anaconda environment check out the video <a href="%5Bhttps://www.youtube.com/watch?v=59hpiFMjhpY%5D(https://www.youtube.com/watch?v=59hpiFMjhpY)">StyleGAN2 installation on GCP</a> 🎥</p>
</li>
<li>
<p>Documentation link to <a href="%5Bhttps://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#viewing-a-list-of-your-environments%5D(https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#viewing-a-list-of-your-environments)">listing out your anaconda environments</a> on Terminal</p>
</li>
</ul>
<h2 id="upload--transfer-learn-from-a-new-model-orange_book-">Upload &amp; Transfer Learn from a new model 📙 <a href="https://youtu.be/Ij1dqSVR89M?t=603">*</a></h2>
<ul>
<li>If your dataset are 🎨 images with dimensions 1200px by 768px, or 768px by 1200px (non-square) you must transfer learn from a model trained on those dimensions.</li>
<li>The model that is default set in transfer learning is 1024px by 1024ox.</li>
<li>You can’t transfer learn if the size of your model and the size of your dataset don’t match.</li>
</ul>
<ol>
<li>Setup Results Folder 📁 to Ignore (“rename”) 🚫 Square Model <a href="https://youtu.be/Ij1dqSVR89M?t=660">*</a></li>
</ol>
<pre><code>mv results/00000-pretrained/network-snapshot-1000.pkl results/00000-pretrained/network-snapshot-1000.pkl-ignore
</code></pre>
<ol start="2">
<li>Get the sharable link to your non-square model pre-trained .pkl file on Google Drive and Gdown the file into the results folder.</li>
</ol>
<pre><code>gdown --id id-ofyour-pkl-file
</code></pre>
<h2 id="train-model-gear-">Train Model ⚙️ <a href="https://youtu.be/Ij1dqSVR89M?t=888">*</a></h2>
<pre><code>!python run_training.py --num-gpus=1 --data-dir=./dataset --config=config-f --dataset=your_dataset_name --mirror-augment=true --metric=none --total-kimg=20000 --min-h=5 --min-w=3 --res-log2=8 --result-dir="/content/drive/My Drive/stylegan2/results"
</code></pre>
<p><strong>Notes</strong></p>
<ul>
<li><em>data-dir</em> should always point to the parent of your parent directory of your TFRecords folder.</li>
<li><em>config</em> use config-e (512px) or config-f (1024px), it depends on the size of the image your are outputting to.</li>
<li><em>dataset</em> input the name of your dataset folder</li>
<li><em>total kimages</em> 20000</li>
<li><em>res-log2</em> means it is a power of 2, so the model will multiply log2-8 by min-width=5 and min-height=2, which gives us our 1280px by 768px training dimensions.</li>
<li>width: 2^6*2  = 768</li>
<li>height=2^8*5  1200</li>
<li>This repo recommends that if you are doing 128 it recommends you use 7</li>
<li>Because that 8th channel although it makes the network a little bit deeper it makes it smaller overall</li>
<li>You can’t do a 16:9 or 720p</li>
</ul>
<h2 id="check-on-your-training-eyes-">Check on Your Training 👀 <a href="https://youtu.be/Ij1dqSVR89M?t=1130">*</a></h2>
<p><img src="https://github.com/Moises404/stylegan2-training-notes/blob/master/Training_NonSquareModel.png" alt="enter image description here"></p>
<ul>
<li>See the line training from your .pkl</li>
<li>We are ready to start training this picks up from this pkl file</li>
<li>Covert some things its a bit slower the first time on the same machine because it is caching some files</li>
<li>Data shape, dynamic shape</li>
<li>Range 0-255 256 the size that we can work with loading networks</li>
<li>Custom Cuda commands compile</li>
<li>(2- 5 minute wait)</li>
<li>Outputting the architecture</li>
<li>Note hub mode works</li>
<li>Building Tensorflow graph</li>
<li>Training for 20k images</li>
<li>In case your dataset the TFRecorsd creation and throw an error here</li>
<li>You will produce a pkl file from its current status</li>
<li>GCP close when i close</li>
<li>Outputting pickling up from the same image</li>
<li>Large of the mini batches</li>
<li>Timing how much memory I’m using underestimates</li>
<li>Ctrl-c</li>
<li>The issue was reactivate the right environment</li>
<li>Run this script</li>
<li>Nohup close this browser window it would stop that command</li>
<li>You could install gnu you could installl gmux</li>
<li>Nohup ,out asses wether this is working</li>
<li>5 mins after</li>
<li>Background in nohup</li>
<li>Essentially it is a background process on the gpu</li>
<li>Nvdia-smi</li>
<li>Cuda version 4.0</li>
<li>How much gpu are you using</li>
<li>Process ID python 15.7gb</li>
<li>This is your command running on the gpu</li>
<li>Kill -9 PID number</li>
</ul>
<h2 id="day-of-training-later..">1 Day of Training Later…</h2>
<ul>
<li>24 hours of training later</li>
<li>Skyflynil folder</li>
<li>Nvdia-smi</li>
</ul>
<p><code>ls results</code><br>
<code>cd/results/0003-stylegan2-your_dataset_name</code></p>
<ul>
<li>80k images later the flower are swirly</li>
<li>500k images gets to a really good point</li>
<li>Truncation value good looking stuff</li>
<li>Download the nohup .out file<br>
<code>ls pwd</code></li>
<li>Download file no-hub.out</li>
<li>Scroll to the bottom</li>
<li>Text output</li>
<li>A tick is a certain number of kimages what you set a mini batch too</li>
<li>How long does it take to train a tick faster with how quickly it takes</li>
</ul>

