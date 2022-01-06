<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Data Nilai Mahasiswa</title>
   <link rel="stylesheet" href="framework/bootstrap/css/bootstr"> 
</head> 
<body>
  <div class="container">
      <div class="row">
          <div class="col-4">
              <form name="frminput">
                  <label for="NIM">NIM</label>
                    <input type="text" class="form-control" id="txNIM">
                    <label for="Kelas"> Kelas</label>
                    <input type="text" class="form-control" id="txKls">
                    <label for="IDPK">Kode Matakuliah</label>
                    <input type="text" class="form-control" id="txIDMK">
                    <div class="form-group sptombol">
                        <button type="button" class="btn btn-primary" id="cari">cari</button>
                    </div>                
                </form> 
            </div>
                <div class="col-4">
                <h2>Data Nilai</h2>
                <div id="lbNIM">NIM: <span id="vtxNIM">: 21101035</span></div>
                <div id="lbnama">Nama<span id="vtxnama">: patris Dedivan  </span></div>
                </div>
                    <h3>Data NILAI</h3>
                    <div  id='VNILAI'></div>
                 </div>
                </div> 
                <div class="col-4">
                <h3>Data  kehadiran</h3>
             <div>
            <div id="VHadir"></div>
        </div>
    </div>
   </div>
</div> 
</body>
<script src="framework/jquery/js/jquery.min.js"></script>
<script>
    $(document).ready(function(){
        $("#cmdcari").click(function(){
            var nim = $("#txNIM").val();
            var kls = $("#txKLS").val();
            var idmk=  $("#txIDMK").val();
            var prm = "getpress-"+idmk+"-"+nim+"-"+kls+".html";
            $.ajax({
                type:"GET",
                url:"https://www.google.com/maps/uv?pb=!1s0x2dd2410294415595%3A0xb9b6c94ad0c08b24!3m1!7e115!4shttps%3A%2F%2Flh5.googleusercontent.com%2Fp%2FAF1QipMz4VpOVmA3-If6NQmDzO8TO2Jb75aS6lzGXCGw%3Dw470-h160-k-no!5skampus%20stiki%20bali%20-%20Penelusuran%20Google!15sCgIgAQ&imagekey=!1e10!2sAF1QipMz4VpOVmA3-If6NQmDzO8TO2Jb75aS6lzGXCGw&hl=id&sa=X&ved=2ahUKEwiLxoH5wp31AhWljuYKHdOhANIQoip6BAgjEAM#"+prm,
                dataType:"json",
                success:function(data){
                    var vnim = ":"+data["NIM"];
                    var vnama= ":"+data["NAMA"];
                    $("#vtxNIM").html(vnim);
                    $("#vtxNAMA").html(vnama);
                    //List Nilai
                    var nnilai = "<ol><ul>Nilai Aktif:"+data["N_AKTIF"]+"</ul><ul>Nilai Tugas:"+data["N_TUGAS"]+"</ul><ul>Nilai Quis:"+data["NQIS"]+"</ul><ul>Nilai UTS:"+data["N_UTS"]+"</ul><ul>Nilai UAS:"+data["N_UAS"]+"</ul><ul>Nilai Akhir:"+data["N_NA"]+"</ul><ul>grade:"+data["GRADE"]+"</ul></ol>";
                    $("#vnilai").html(nnilai);
                    //List Kehadiran
                    var jmlpertemuan = 16;
                    var jhadir = jmlpertemuan - parseint(data["MANGKIR"]);
                    var hadir = "<h3>Presensi</h3>jumlah Tidak kehadiran: "+jhadir+"("+data["PROSES_HADIR"]+")";
                    $("#vhadir").html(hadir);
                }

            });
         });
    });
        
           
</script>
 </html>
