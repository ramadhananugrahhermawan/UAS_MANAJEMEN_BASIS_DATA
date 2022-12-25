# UAS_MANAJEMEN_BASIS_DATA

### Kelompok 6 
- Rafi Andamira (1207050098)
- Raihan (1207050099)
- Ramadhan Anugrah Hermawan (1207050101)

# Cara Install Laravel

## ada beberapa hal yang perlu Anda siapkan dan install terlebih dahulu untuk mendukung instalasi Laravel di Windows.
Aplikasi pendukung tersebut adalah :
- Aplikasi XAMPP (Download Xampp)
- Composer (Download Composer)

# Cara install Laravel di Windows terdiri dari beberapa langkah, yaitu:

1. Masuk ke Command Prompt atau CMD
Setelah itu arahkan CMD atau terminal Anda agar berada di dalam direktori file server.
Lokasi file server di XAMPP sendiri secara default yaitu di xampp/htdocs. Anda hanya perlu
memasukkan perintah dibawah ini untuk masuk ke direktori htdocs.

2. Mulai Install Laravel
Jika Anda sudah masuk ke direktori htdocs, Anda perlu mengambil sekaligus install file
Laravel yang berada di dalam repositori Github. Masukkan perintah ini di terminal anda :
composer create-project --prefer-dist laravel/laravel nama_projectmu
tunggu hingga proses instalasi selesai

3. Cek Instalasi Framework Laravel di Browser
Jika Anda ingin memastikan Laravel sudah terinstall atau belum, Anda bisa arahkan
Command Prompt ke direktori yang sudah dibuat sebelumnya. Setelah itu, gunakan kode
dibawah ini:
php artisan serve
Jika di terminal Anda terlihat tulisan Laravel development server started setelah Anda
gunakan kode tersebut, maka selanjutnya Anda bisa buka link yang tampil tersebut di
browser. Default nya yaitu 127.0.0.1:8000. Nanti di homepage tersebut akan muncul tulisan
Laravel.

4. Buat database di MySQL
Buka terlebih dahulu XAMPP dan jalankan MySQL Database serta Apache nya
Lalu buka pada browser http://localhost/phpmyadmin/
Buat database baru bernamakan bebas sesuai keinginan (disini kami menamainya
lashoped)
Jika sudah tinggal membuat tabel dari isi database yang akan dibuat

5. Konfgurasi Database

Sebagai contoh di project kita kali ini, katakanlah nama database yang akan kita
pakai itu db_blog, lalu credential mysql di laptop kita itu usernamenya itu admin dan
passwordnya itu password.



APP_NAME=Laravel
APP_ENV=local
APP_KEY=base64:tq52gB69KxTaiaxY/FgCil/O+dq8EHNWLyHojq7emyQ=
APP_DEBUG=true
APP_URL=http://localhost

LOG_CHANNEL=stack

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=lashoped
DB_USERNAME=root
DB_PASSWORD=

BROADCAST_DRIVER=log
CACHE_DRIVER=file
QUEUE_CONNECTION=sync
SESSION_DRIVER=file
SESSION_LIFETIME=120

REDIS_HOST=127.0.0.1
REDIS_PASSWORD=null
REDIS_PORT=6379

MAIL_DRIVER=smtp
MAIL_HOST=smtp.mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=null
MAIL_PASSWORD=null
MAIL_ENCRYPTION=null

AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=

PUSHER_APP_ID=
PUSHER_APP_KEY=
PUSHER_APP_SECRET=
PUSHER_APP_CLUSTER=mt1

MIX_PUSHER_APP_KEY="${PUSHER_APP_KEY}"
MIX_PUSHER_APP_CLUSTER="${PUSHER_APP_CLUSTER}"


6. Membuat Model dan Migration
Di langkah ini kita akan mencoba membuat model dan migration dengan satu artisan command. Kita buka kembali terminal atau cmd, kita jalankan artisan command di bawah ini.

php artisan make:model Post -m

Kita bisa lihat ada dua file yang berhasil digenerate menggunakan command di atas, yang pertama adalah file model app/Models/Post.php dan yang kedua file migration database/migrations/2021_08_18_043743_create_posts_table.php. Sebagai catatan nama file migration itu disesuaikan dengan tanggal pada saat file migration itu dibuat.

7. Membuat BackEnd



- CREATE
Untuk menambahkan data source code nya sepeerti dibawah ini : 


<?php

namespace App\Http\Controllers;
use App\Barang;
use Auth;
use Alert;
use Carbon\Carbon;
use Illuminate\Http\Request;

class TambahController extends Controller
{
	public function __construct()
    {
        $this->middleware('auth');
    }

    public function index()
    {
    	return view('tambah.index');
    }

    public function tambah(Request $request)
    {
    	$this->validate($request, 
           [
            'nama_barang'=>'required',
            'harga'=>'required',
            'stok'=>'required',
            'keterangan'=>'',
            'gambar'=>''
            ]);

        $barang = new \App\Barang;
        $barang->nama_barang = $request->nama_barang;
        $barang->harga = $request->harga;
        $barang->stok = $request->stok;
        $barang->keterangan = $request->keterangan;
        $barang->gambar = $request->gambar;
        $barang->save();

        Alert()->success('Barang Sukses Ditambah!', 'Success');
        return redirect('tambah');

    }
}

- UPDATE
Untuk mengupdate data source code nya seperti dibawah ini 


<?php

namespace App\Http\Controllers;
use App\Barang;
use App\Pesanan;
use App\User;
use App\PesananDetail;
use Auth;
use Alert;
use Carbon\Carbon;
use Illuminate\Http\Request;

class HistoryController extends Controller
{
    public function __construct()
    {
        $this->middleware('auth');
    }

    public function index()
    {
    	$pesanans = Pesanan::where('user_id', Auth::user()->id)->where('status', '!=',0)->get();

    	return view('history.index', compact('pesanans'));
    }

    public function detail($id)
    {
    	$pesanan = Pesanan::where('id', $id)->first();
    	$pesanan_details = PesananDetail::where('pesanan_id', $pesanan->id)->get();
    	
    	return view('history.detail', compact('pesanan','pesanan_details'));
    }

}

- DELETE
Untuk menghapus data source codenya seperti dibawah ini yang diblock berwarna biru 

@extends('layouts.app')
@section('content')
<div class="container">
  <div class="row">
  	<div class="col-md-12">
  		<a href="{{ url('home') }}" class="btn btn-primary"><i class="far fa-arrow-alt-circle-left"></i> Kembali</a>
  	</div>
  	
    <div class="col-md-12 mt-3">
  		<nav aria-label="breadcrumb">
  			<ol class="breadcrumb">
         <li class="breadcrumb-item"><a href="{{ url('home') }}">Home</a></li>
         <li class="breadcrumb-item active" aria-current="page">Check Out</li>
       </ol>
     </nav>
   </div>
   
   <div class="col-md-12">
    <div class="card">
      <div class="card-body">
        <h3><i class="fa fa-shopping-cart"></i> Check Out</h3>
        @if(!empty($pesanan))
        <p align="right">Tanggal Pesan : {{ $pesanan->tanggal }}</p>
        <table class="table table-striped">
          <thead>
            <tr>
              <th>No</th>
              <th>Gambar</th>
              <th>Nama Barang</th>
              <th>Jumlah</th>
              <th>Harga</th>
              <th>Total Harga</th>
              <th>Aksi</th>
            </tr>
          </thead>
          <tbody>
            <?php $no = 1; ?>
            @foreach($pesanan_details as $pesanan_detail)
            <tr>
              <td>{{ $no++ }}</td>
              <td>
                <img src="{{ url('uploads') }}/{{ $pesanan_detail->barang->gambar }}" width="100" alt="...">
              </td>
                <td>{{ $pesanan_detail->barang->nama_barang }}</td>
                <td>{{ $pesanan_detail->jumlah }} sepatu</td>
                <td align="right">Rp. {{ number_format($pesanan_detail->barang->harga) }}</td>
                <td align="right">Rp. {{ number_format($pesanan_detail->jumlah_harga) }}</td>
              <td>
                <form action="{{ url('check-out') }}/{{ $pesanan_detail->id }}" method="post">
                  @csrf
                  {{ method_field('DELETE') }}
                  <button type="submit" class="btn btn-danger btn-sm" onclick="return confirm('Anda yakin akan menghapus data?');"><i class="far fa-trash-alt"></i></button>
                </form>
              </td>
            </tr>
            <tr>
              <td colspan="5" align="right"><strong>Total Harga : </strong></td>
              <td align="right"><strong>Rp. {{ number_format($pesanan_detail->jumlah_harga) }}</strong></td>
              <td>
                <a href="{{ url('konfirmasi-check-out') }}" class="btn btn-success" onclick="return confirm('Anda yakin akan Check Out?');">
                  <i class="fas fa-shopping-cart"></i> Check Out
                </a>
              </td>
            </tr>
            @endforeach
          </tbody>
        </table>
        @endif
      </div>
    </div>
  </div>
</div>
</div>
@endsection










