# Memulai Git #

Bab ini berisi pendahuluan mengenai Git. Kita akan memulai dengan membahas sedikit mengenai latar belakang sejarah version control, kemudian berlanjut pada tata cara menjalankan Git pada sistem Anda dan terakhir cara untuk melakukan penyetingan dan memulai bekerja dengan Git. Pada akhir dari bab ini, diharapkan Anda dapat memahami mengapa Git ada, kenapa Anda harus menggunakannya dan harus melakukan pengaturan untuk menggunakannya.

## Tentang Version Control ##

Apa itu version control, dan kenapa Anda harus peduli? Version control adalah sebuah sistem yang mencatat setiap perubahan terhadap sebuah berkas atau kumpulan berkas sehingga pada suatu saat Anda dapat kembali kepada salah satu versi dari berkas tersebut. Sebagai contoh dalam buku ini Anda akan menggunakan kode sumber perangkat lunak sebagai berkas yang akan dilakukan version controlling, meskipun pada kenyataannya Anda dapat melakukan ini pada hampir semua tipe berkas di komputer.

Jika Anda adalah seorang desainer grafis atau desainer web dan Anda ingin menyimpan setiap versi dari gambar atau layout yang Anda buat (kemungkinan besar Anda pasti ingin melakukannya), maka Version Control System (VCS) merupakan sebuah solusi bijak untuk digunakan. Sistem ini memungkinkan Anda untuk mengembalikan berkas Anda pada kondisi/keadaan sebelumnya, mengembalikan seluruh proyek pada keadaan sebelumnya, membandingkan perubahan setiap saat, melihat siapa yang terakhir melakukan perubahan terbaru pada suatu objek sehingga berpotensi menimbulkan masalah, siapa yang menerbitkan isu, dan lainnya. Dengan menggunakan VCS dapat berarti jika Anda telah mengacaukan atau kehilangan berkas, Anda dapat dengan mudah mengembalikannya. Ditambah lagi, Anda mendapatkan semua ini dengan overhead yang sangat sedikit.

### Version Control System Lokal ###

Kebanyakan orang melakukan pengontrolan versi dengan cara menyalin berkas-berkas pada direktori lain (mungkin dengan memberikan penanggalan pada direktori tersebut, jika mereka rajin). Metode seperti ini sangat umum karena sangat sederhana, namun cenderung rawan terhadap kesalahan. Anda akan sangat mudah lupa dimana direktori Anda sedang berada, selain itu dapat pula terjadi ketidak sengajaan penulisan pada berkas yang salah atau menyalin pada berkas yang bukan Anda maksudkan.

Untuk mengatasi permasalahan ini, para programmer mengembangkan berbagai VCS lokal yang memiliki sebuah basis data sederhana untuk menyimpan semua perubahan pada berkas yang berada dalam cakupan revision control (Lihat Gambar 1-1).

Insert 18333fig0101.png 
Gambar 1-1. Diagram version control lokal.

Salah satu perkakas VCS yang populer adalah rcs, kakas ini masih didistribusikan dengan berbagai komputer pada masa kini. Bahkan sistem operasi Mac OS X menyertakan rcs ketika menginstal Developer Tools. Kakas ini pada dasarnya bekerja dengan cara menyimpan kumpulan patch dari satu perubahan ke perubahan lainnya dalam format khusus pada disk; ini kemudian dapat digunakan untuk menciptakan kembali wujud/keadaan suatu berkas pada suatu saat dengan cara menggunakan patch yang berkesesuaian dengan berkas dan waktu yang diinginkan.

### Version Control Systems Terpusat ###

Permasalahan berikutnya yang dihadapi adalah para pengembang perlu melakukan kolaborasi dengan pengembang pada sistem lainnya. Untuk mengatasi permasalahan ini maka dibangunlah Centralized Version Control Systems (CVCSs). Sistem ini, diantaranya CVS, Subversion, dan Perforce, memiliki sebuah server untuk menyimpan setiap versi berkas, dan beberapa klien yang dapat melakukan checkout berkas dari server pusat. Untuk beberapa tahun, sistem seperti ini menjadi standar untuk version control (lihat Gambar 1-2).

Insert 18333fig0102.png 
Gambar 1-2. Diagram version control terpusat.

Sistem seperti ini memiliki beberapa kelebihan, terutama jika dibandingkan dengan VCS lokal. Misalnya, setiap orang pada tingkat tertentu mengetahui apa yang orang lain lakukan pada proyek. Administrator memiliki kendali yang mantap atas siapa yang dapat melakukan apa; dan adalah jauh lebih mudah untuk mengelola sebuah CVCS dibandingkan menangani database lokal pada setiap client.

Walau demikian, sistem dengan tatanan seperti ini memiliki kelemahan serius. Kelemahan nyata yang direpresesntasikan oleh sistem dengan server terpusat. Jika server mati untuk beberapa jam, maka tidak ada seorangpun yang bisa berkolaborasi atau menyimpan perubahan terhadap apa yang mereka telah kerjakan. Jika harddisk yang menyimpan basis data mengalami kerusakan, dan salinan yang beran belum tersimpan, Anda akan kehilangan setiap perubahan dari proyek kecuali snapshot yang dimiliki oleh setiap kolaborator pada komputernya masing-masing. VCS lokal juga mengalami nasib yang sama jika Anda menyimpan seluruh history perubahan proyek pada satu tempat, Anda mempunyai resiko kehilangan semuanya. 

### Version Control System Terdistribusi ###

Inilah saatnya bagi Distributed Version Control Systems untuk mengambil tempat. dalam sebuah DVCS (seperti Git, Mercurial, Bazaar atau Darcs), klien tidak hanya melakukan checkout untuk snapshot terakhir setiap berkas, namun mereka (klien) memiliki salinan penuh dari repositori tersebut. Jadi, jika server mati, dan sistem berkolaborasi melalui server tersebut, maka klien manapun dapat mengirimkan salinan repositori tersebut kembali ke server. Setiap checkout pada DVCS merupakan sebuah backup dari keseluruhan data (lihat Gambar 1-3).

Insert 18333fig0103.png 
Gambar 1-3. Diagram distributed version control.

Lebih jauh lagi, kebanyakan sistem seperti ini mampu menangani sejumlah remote repository dengan baik, jadi Anda dapat melakukan kolaborasi dengan berbagai kelompok kolaborator dalam berbagai cara secara bersama-sama pada suatu proyek. Hal ini memungkinkan Anda untuk menyusun beberapa jenis alur kerja yang tidak mungkin dilakukan pada sistem terpusat, seperti hierarchical model. 

## Sejarah Singkat Git ##

Seperti hal besar lainnya, Git diawali dengan sedikit permasalahan dan kontroversi. Kernel Linux merupakan sebuah proyek perangkat lunak open source skala besar. Sepanjang perjalanan perawatan Kernel Linux (1991-2002), perubahan disimpan sebagai patch dan arsip-arsip berkas. Pada tahun 2002, proyek ini mulai menggunakan sebuah DVCS proprietary bernama BitKeeper.

Pada tahun 2005, hubungan antara komunitas pengembang Kernel Linux dengan perusahan yang mengembangkan Bitkeeper retak, dan status "gratis" pada BitKeeper dicabut. Hal ini membuat komunitas pengembang Kernel Linux (dan khususnya Linus Torvalds, sang pencipta Linux) harus mengembangkan perkakas sendiri dengan berbekal pengalaman yang mereka peroleh ketika menggunakan BitKeeper. Dan sistem tersebut diharapkan dapat memenuhi beberapa hal berikut:

* Kecepatan
* Desain yang sederhana
* Dukungan penuh untuk pengembangan non-linear (ribuan cabang paralel)
* Terdistribusi secara penuh
* Mampu menangani proyek besar seperti Kernel Linux secara efisien (dalam kecepatan dan ukuran data)

Sejak kelahirannya pada tahun 2005, Git telah berkembang dan semakin mudah digunakan serta hingga saat ini masih mempertahankan kualitasnya tersebut. Git luar biasa cepat, sangat efisien dalam proyek besar, dan memiliki sistem pencabangan yang luar biasa untuk pengembangan non-linear (Lihat Bab 3).

## Dasar Git ##

Jadi, sebenarnya apa yang dimaksud dengan Git? Ini adalah bagian penting untuk dipahami, karena jika Anda memahami apa itu Git dan cara kerjanya, maka dapat dipastikan Anda dapat menggunakan Git secara efektif dengan mudah. Selama mempelajari Git, cobalah untuk melupakan VCS lain yang mungkin telah Anda kenal sebelumnya, misalnya Subversion dan Perforce. Git sangat berbeda dengan sistem-sistem tersebut dalam hal menyimpan dan memperlakukan informasi yang digunakan, walaupun antar-muka penggunanya hampir mirip. Dengan memahami perbedaan tersebut diharapkan dapat membantu Anda menghindari kebingungan saat menggunakan Git.

### Snapshot, Bukan Perbedaan ###

Salah satu perbedaan yang mencolok antar Git dengan VCS lainnya (Subversion dan kawan-kawan) adalah dalam cara Git memperlakukan datanya. Secara konseptual, kebanyakan sistem lain menyimpan informasi sebagai sebuah daftar perubahan berkas. Sistem seperti ini (CVS, Subversion, Bazaar, dan yang lainnya) memperlakukan informasi yang disimpannya sebagai sekumpulan berkas dan perubahan yang terjadi pada berkas-berkas tersebut, sebagaimana yang diperlihatkan pada Gambar 1-4.

Insert 18333fig0104.png 
Gambar 1-4. Sistem lain menyimpan data perubahan terhadap versi awal setiap berkas.

Git tidak bekerja seperti ini. Melainkan, Git memperlakukan datanya sebagai sebuah kumpulan snapshot dari sebuah miniatur sistem berkas. Setiap kali Anda melakukan commit, atau melakukan perubahan pada proyek Git Anda, pada dasarnya Git merekam gambaran keadaan berkas-berkas Anda pada saat itu dan menyimpan referensi untuk gambaran tersebut. Agar efisien, jika berkas tidak mengalami perubahan, Git tidak akan menyimpan berkas tersebut melainkan hanya pada file yang sama yang sebelumnya telah disimpan. Git memperlakukan datanya seperti terlihat pada Gambar 1-5.

Insert 18333fig0105.png 
Gambar 1-5. Git menyimpan datanya sebagai snapshot dari proyek setiap saat.

Ini adalah sebuah perbedaan penting antara Git dengan hampir semua VCS lain. Hal ini membuat Git mempertimbangkan kembali hampir setiap aspek dari version control yang oleh kebanyakan sistem lainnya disalin dari generasi sebelumnya. Ini membuat Git lebih seperti sebuah miniatur sistem berkas dengan beberapa tool yang luar biasa ampuh yang dibangun di atasnya, ketimbang sekadar sebuah VCS. Kita akan mempelajari beberapa manfaat yang Anda dapatkan dengan memikirkan data Anda dengan cara ini ketika kita membahas "Git branching" pada Bab 3.

### Hampir Semua Operasi Dilakukan Secara Lokal ###

Kebanyakan operasi pada Git hanya membutuhkan berkas-berkas dan resource lokal – tidak ada informasi yang dibutuhkan dari komputer lain pada jaringan Anda. Jika Anda terbiasa dengan VCS terpusat dimana kebanyakan operasi memiliki overhead latensi jaringan, aspek Git satu ini akan membuat Anda berpikir bahwa para dewa kecepatan telah memberkati Git dengan kekuatan. Karena Anda memiliki seluruh sejarah dari proyek di lokal disk Anda, dengan kebanyakan operasi yang tampak hampir seketika.

Sebagai contoh, untuk melihat history dari proyek, Git tidak membutuhkan data histori dari server untuk kemudian menampilkannya untuk Anda, namun secara sedarhana Git membaca historinya langsung dari basis data lokal proyek tersebut. Ini berarti Anda melihat histori proyek hampir secara instant. Jika Anda ingin membandingkan perubahan pada sebuah berkas antara versi saat ini dengan versi sebulan yang lalu, Git dapat mencari berkas yang sama pada sebulan yang lalu dan melakukan pembandingan perubahan secara lokal, bukan dengan cara meminta remote server melakukannya atau meminta server mengirimkan berkas versi yang lebih lama kemudian membandingkannya secara lokal.

Hal ini berarti bahwa sangat sedikit yang tidak bisa Anda kerjakan jika Anda sedang offline atau berada di luar VPN. Jika Anda sedang berada dalam pesawat terbang atau sebuah kereta dan ingin melakukan pekerjaan kecil, Anda dapat melakukan commit sampai Anda memperoleh koneksi internet hingga Anda dapat menguploadnya. Jika Anda pulang ke rumah dan VPN client Anda tidak bekerja dengan benar, Anda tetap dapat bekerja. Pada kebanyakan sistem lainnya, melakukan hal ini cukup sulit atau bahkan tidak mungkin sama sekali. Pada Perforce misalnya, Anda tidak dapat berbuat banyak ketika Anda tidak terhubung dengan server; pada Subversion dan CVS, Anda dapat mengubah berkas, tapi Anda tidak dapat melakukan commit pada basis data Anda (karena Anda tidak terhubung dengan basis data). Hal ini mungkin saja bukanlah masalah yang besar, namun Anda akan terkejut dengan perbedaan besar yang disebabkannya.

### Git Memiliki Integritas ###

Segala sesuatu pada Git akan melalui proses checksum terlebih dahulu sebelum disimpan yang kemudian direferensikan oleh hasil checksum tersebut. Hal ini berarti tidak mungkin melakukan perubahan terhadap berkas manapun tanpa diketahui oleh Git. Fungsionalitas ini dimiliki oleh Git pada level terendahnya dan ini merupakan bagian tak terpisahkan dari filosofi Git. Anda tidak akan kehilangan informasi atau mendapatkan file yang cacat tanpa diketahui oleh Git.

Mekanisme checksum yang digunakan oleh Git adalah SHA-1 hash. Ini merupakan sebuah susunan string yang terdiri dari 40 karakter heksadesimal (0 hingga 9 dan a hingga f) dan dihitung berdasarkan isi dari sebuah berkas atau struktur direktori pada Git. sebuah hash SHA-1 berupa seperti berikut:

	24b9da6552252987aa493b52f8696cd6d3b00373

Anda akan melihat nilai seperti ini pada berbagai tempat di Git. Faktanya, Git tidak menyimpan nama berkas pada basis datanya, melainkan nilai hash dari isi berkas.

### Secara Umum Git Hanya Menambahkan Data ###

Ketika Anda melakukan operasi pada Git, kebanyakan dari operasi tersebut hanya menambahkan data pada basis data Git. Hal ini sangat sulit membuat sistem untuk melakukan semuanya yang tidak bisa dibatalkan atau membuat sistem menghapus data dengan berbahai cara. Seperti pada berbagai VCS, Anda dapat kehilangan atau mengacaukan perubahan yang belum di-commit; namun jika Anda melakukan commit pada Git, akan sangat sulit kehilangannya, terutama jika Anda secara teratur melakukan push basis data Anda pada repositori lain.

Hal ini menjadikan Git menyenangkan karena kita dapat berexperimen tanpa kehawatiran untuk mengacaukan proyek. Untuk lebih jelas dan dalam lagi tentang bagaimana Git menyimpan datanya dan bagaimana Anda dapat mengembalikan yang hilang, lihat "Under the Covers" pada Bab 9.

### Tiga Keadaan ###

Sekarang perhatikan. Ini adalah hal utama yang harus diingat tentang Git jika Anda ingin proses belajar Anda berjalan lancar. Git memiliki 3 keadaan utama dimana berkas Anda dapat berada: committed, modified dan staged. Committed berarti data telah tersimpan secara aman pada basis data lokal. Modified berarti Anda telah melakukan perubahan pada berkas namun Anda belum melakukan commit pada basis data. Staged berarti Anda telah menAndai berkas yang telah diubah pada versi yang sedang berlangsung untuk kemudian dilakukan commit.

Ini membawa kita ke tiga bagian utama dari sebuah projek Git: direktori Git, direktori kerja, dan staging area.

Insert 18333fig0106.png 
Figure 1-6. Direktori kerja, staging area, dan direktori git.

Direktori Git adalah dimana Git menyimpan metadata dan database objek untuk projek Anda. Ini adalah bahagian terpenting dari Git, dan inilah yang disalin ketika Anda melakukan kloning sebuah repository dari komputer lain.

Direktori kerja adalah sebuah checkout tunggal dari satu versi dari projek. Berkas-berkas ini kemudian ditarik keluar dari basis data yang terkompresi dalam direktori Git dan disimpan pada disk untuk Anda gunakan atau modifikasi.

Staging area adalah sebuah berkas sederhana, umumnya berada dalam direktori Git Anda, yang menyimpan informasi mengenai apa yang menjadi commit selanjutnya. Ini terkadang disebut sebagai index, tetapi semakin menjadi stAndard untuk menyebutnya sebagai staging area.

Alur kerja dasar Git adalah seperti ini:

1.	Anda mengubah berkas dalam direktori kerja Anda.
2.	Anda membawa berkas ke stage, menambahkan snapshot-nya ke staging area.
3.	Anda melakukan commit, yang mengambil berkas seperti yang ada di staging area dan menyimpan snapshotnya secara permanen ke direktori Git Anda.

Jika sebuah versi tertentu dari sebuah berkas telah ada di direktori git, ia dianggap 'committed'. Jika berkas diubah (modified) tetapi sudah ditambahkan ke staging area, maka berkas tersebut adalah 'staged'. Dan jika berkas telah diubah sejak terakhir dilakukan checked out tetapi belum ditambahkan ke staging area maka itu adalah 'modified'. Pada Bab 2, Anda akan mempelajari lebih lanjut mengenai keadaan-keadaan ini dan bagaimana Anda dapat memanfaatkan keadaan-keadaan tersebut ataupun melewatkan bagian 'staged' seluruhnya.

## Menginstall Git ##

Mari memulai menggunakan Git. Pertama, tentu saja Anda harus menginstallnya terlebih dahulu. Anda dapat melakukan melalui berbagai cara; dua cara paling poluler adalah menginstallnya dari kode sumbernya atau menginstalkan paket yang telah disediakan untuk platform Anda.

### Menginstall Dari Kode Sumber ###

Jika Anda dapat melakukannya, akan sangat berguna untuk dapat menginstallnya dari kode sumber, karena Anda akan mendapatkan versi terbaru dari Git. Setiap versi dari Git cenderung akan menampilkan kemajuan pada sisi antarmuka pengguna, jadi menggunakan versi terbaru seringkali menjadi jalan terbaik jika Anda terbiasa melakukan kompilasi perangkat lunak dari kode sumbernya. Dan juga menjadi masalah bahwa banyak distribusi Linux yang menyertakan versi Git yang sangat lama; kecuali Anda mempergunakan distribusi Linux paling up-to-date atau menggunakan backport, menginstall dari kode sumbernya mungkin menjadi solusi terbaik.

Untuk menginstall Git, Anda membutuhkan beberapa library yang dibutuhkan oleh Git: curl, zlib, openssl, expat, dan libiconv. Sebagai contoh, jika Anda berada pada sistem yang menggunakan yum (seperti Fedora) atau apt-get (seperti sistem berbasis Debian), Anda dapat menggunakan salah satu dari perintah berikut untuk menginstall semua library yang dibutuhkan oleh Git:

	$ yum install curl-devel expat-devel gettext-devel \
	  openssl-devel zlib-devel

	$ apt-get install libcurl4-gnutls-dev libexpat1-dev gettext \
	  libz-dev

Setelah Anda memperoleh semua library yang dibutuhkan, Anda kemudian dapat melanjutkan dengan mengunduh Git dari situsnya:

	http://git-scm.com/download
	
Kemudian, kompilasi dan install:

	$ tar -zxf git-1.6.0.5.tar.gz
	$ cd git-1.6.0.5
	$ make prefix=/usr/local all
	$ sudo make prefix=/usr/local install

Setelah semua ini selesai, Anda juga dapat memperoleh Git terbaru melalui Git sendiri:

	$ git clone git://git.kernel.org/pub/scm/git/git.git
	
### Menginstall Git di Linux ###

Jika Anda ingin menginstall Git di Linux menggunakan installer biner, Anda bisa melakukannya melalui perkakas manajemen paket yang Anda pada distribusi Linux yang Anda gunakan. Jika Anda menggunakan Fedora, Anda dapat menggunakan yum:

	$ yum install git-core

Atau jika Anda menggunakan distro berbasis Debian seperti Ubuntu, coba gunakan apt-get:

	$ apt-get install git-core

### Menginstall Git pada Mac ###

Terdapat dua cara mudah untuk menginstal Git pada sebuah komputer Mac. Cara termudah adalah menggunakan installer Git berbasis GUI, yang dapat Anda peroleh dari halaman Google Code (lihat Gambar 1-7):

	http://code.google.com/p/git-osx-installer

Insert 18333fig0107.png 
Gambar 1-7. Git OS X installer.

Cara lainnya adalah dengan menggunakan MacPorts (`http://www.macports.org`). Jika Anda telah menginstall MacPorts, maka Anda dapat menginstall Git melalui cara berikut

	$ sudo port install git-core +svn +doc +bash_completion +gitweb

Anda tidak harus menambahkan extras-nya, tetapi Anda mungkin membutuhkan +svn jika Anda harus menggunakan Git pada repositori Subversion (lihat Bab 8).

### Menginstall pada Sistem Operasi Windows ###

Menginstall Git pada Windows sangatlah mudah. Cara termudah dapat Anda peroleh dengan menggunakan msysGit. Cukup download file installernya dari halaman Google Code, lalu eksekusi.

	http://code.google.com/p/msysgit

Setelah terinstall, Anda akan memperoleh versi command-line (bersama dengan klien SSH yang praktis) dan versi GUI-nya.

## Setup Git Untuk Pertama Kalinya ##

Sekarang Anda telah memiliki Git pada sistem Anda, berikutnya Anda akan harus melakukan beberapa penyesuai pada lingkungan Git Anda. Anda hanya perlu melakukan hal ini sekali saja; pada saat memperbaharui versi Git Anda, penyesuai tidak perlu dilakukan lagi. Anda pun dapat mengubah penyesuaian tersebut setiap saat.

Pada Git terdapat sebuah perkakas yang disebut dengan git config yang memungkinkan Anda untuk memperoleh informasi dan menetapkan variabel konfigurasi yang mengontrol segala aspek bagaimana Git beroperasi dan berperilaku. Variabel-variabel ini dapat disimpan pada tiga tempat berbeda:

*	`/etc/gitconfig` file: Menyimpan berbagai nilai-nilai variabel untuk setiap pengguna pada sistem dan semua repositori milik para pengguna tersebut. Jika Anda memberikan opsi `--system` pada `git config`, maka Git akan membaca dan menulis file konfigurasi ini secara spesifik.
*	`~/.gitconfig` file: Spesifik hanya untuk pengguna yang bersangkutan. Anda dapat membuat Git membaca dan menulis pada berkas ini secara spesifik dengan memberikan opsi `--global`. 
*	config file pada direktori git (yaitu, `.git/config`) atau reposotori manapun yang sedang Anda gunakan: Spesifik hanya pada repositori itu saja. Setiap nilai pada setiap tingkat akan selalu menimpa nilai yang telah ditetapkan pada level sebelumnya, jadi nilai yang telah di-set pada `.git/config` akan menimpa nilai yang telah di-set pada `/etc/gitconfig`.

Pada Sistem Operasi Windows, Git akan mencari berkas `.gitconfig` pada direktori `$HOME` (`C:\Documents and Settings\$USER` untuk kebanyakan kasus). Selain itu juga akan mencari /etc/gitconfig, direktori ini relatif terhadap direktori root MSys, yang mana tergantung dari direktori yang dipilih saat Anda menginstall Git pada Windows Anda.

### Identitas Anda ###

Hal pertama yang harus Anda lakukan ketika menginstalkan Git adalah mengatur username dan alamat email Anda. Hal ini penting karena setiap commit pada Git akan menggunakan informasi ini, dan informasi ini akan selamanya disimpan dengan commit yang Anda buat tersebut:

	$ git config --global user.name "John Doe"
	$ git config --global user.email johndoe@example.com

Lagi-lagi, Anda hanya perlu melakukan ini sekali saja jika Anda menggunakan opsi `--global`, karena Git akan selalu menggunakan informasi tersebut selama Anda berada pada sistem yang sama. Jika Anda ingin menimpa informasi ini dengan menggunakan email atau username yang berbeda untuk proyek tertentu, Anda dapat perintah tersebut tanpa menggunakan opsi `--global` ketika Anda berada pada proyek tersebut.

### Editor Anda ###

Sekarang identitas Anda telah siap, berikutnya Anda dapat memilih text editor default yang akan digunakan manakala Git membutuhkan Anda untuk menulis sebuah pesan. Secara default, Git akan menggunakan default editor sesuai dengan sistem operasi, biasanya adalah Vi atau Vim pada sistem Unix. Jika Anda ingin menggunakan text editor yang lainnya, seperti Emacs, Anda dapat melakukan perintah seperti berikut:

	$ git config --global core.editor emacs
	
### Perkakas Diff Anda ###

Opsi lainnya yang mungkin berguna dan mungkin ingin Anda ubah adalah perkakas diff yang digunakan untuk menyelesaikan konflik yang terjadi ketika dilakukannya merge (penggabungan). Katakanlah Anda ingin menggunakan vimdiff:

	$ git config --global merge.tool vimdiff

Git dapat menggunakan berbagai perkakas diff ini diantaranya kdiff3, tkdiff, meld, xxdiff, emerge, vimdiff, gvimdiff, ecmerge, dan opendiff. Anda pun dapat menggunakan perkakas kastem; lihat Bab 7 untuk informasi lebih jauh lagi mengenai hal tersebut.

### Mengecek Settingan Anda ###

Jika Anda ingin mengecek settingan Anda, Anda dapat menggunakan peritah `git config --list` untuk menampilkan semua settingan yang digunakan Git:

	$ git config --list
	user.name=Scott Chacon
	user.email=schacon@gmail.com
	color.status=auto
	color.branch=auto
	color.interactive=auto
	color.diff=auto
	...

Anda mungkin akan melihat beberapa variabel yang ditampilkan lebih dari sekali, hal ini terjadi karena variabel yang sama diperoleh dari beberapa file konfigurasi berbeda (misalnya, `/etc/gitconfig` dan `~/.gitconfig`). Pada kasus seperti ini, Git hanya akan menggunakan nilai yang terlihat paling akhir saja.

Andapun dapat melihat apa nilai yang Git pergunakan untuk suatu variabel secara spesifik dengan mengunakan `git config {key}`:

	$ git config user.name
	Scott Chacon

## Memperoleh Bantuan ##

Jika Anda membutuhkan bantuan ketika menggunakan Git, terdapat 3 cara yang dapat digunakan untuk membuka halaman manual (manpage) untuk setiap perintah Git:

	$ git help <verb>
	$ git <verb> --help
	$ man git-<verb>

Sebagai contoh, Anda dapat memperoleh halaman manual untuk perintah config dengan menjalankan perintah:

	$ git help config

Perintah ini sangatlah luar biasa karena Anda dapat mengaksesnya kapan saja, bahkan ketika sedang offline.
Jika manpage (halaman manual) dan buku ini tidaklah cukup, dan Anda membutuhkan pertolongan dari seorang manusia, Anda dapat mencoba channel `#git` atau `#github` pada Freenode IRC server (irc.freenode.net). Channel ini biasanya berisi ratusan orang yang memiliki pengetahuan tentang Git dan sering kali memiliki kemauan untuk menolong.

## Kesimpulan ##

Sekarang Anda memiliki pengetahuan dasar mengenai apa yang dimaksud dengan Git dan perbedaannya dari centralized VCS yang mungkin pernah Anda gunakan. Anda pun seharusnya sekarang memiliki Git pada sistem Anda yang telah diatur dengan identitas personal Anda. Sekarang saatnya untuk Anda mempelajari beberapa dasar Git.
