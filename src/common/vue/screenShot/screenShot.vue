<template>
<div class="screenShotContent">
  <div style="height:5px;"></div>
  <div id="ctlDiv">
    <a id="btnCapture" href="javascript:StartCapture()" class="btn">屏幕截图</a>

    <a id="btnReload" href="javascript:ReloadPlugin()" class="btn" style="display:none">正在进行插件安装，安装成功后请点击这里...</a>
    <input type="checkbox" id="hideCurrent" value="0"><label for="hideCurrent">自动最小化当前窗口</label>
    <input type="checkbox" id="autoupload" value="0"><label for="autoupload">截图完成后自动上传</label>
    <input type="checkbox" id="captureselectSize" value="0"><label for="captureselectSize">更多个性化截图选择</label>
  </div>
  <div id="moreparams" style="padding-left:118px;height:30px;" >
    <div style="position: relative; float:left;">
      <input type="radio" name="radioselect" id="getimagefromclipboard"  /><label for="getimagefromclipboard">从剪贴板获取图片</label>
      <input type="radio" name="radioselect" id="showprewindow" checked="checked" /><label for="showprewindow">截图时弹出提示窗口</label>
      <input type="radio" name="radioselect" id="fullscreen" checked="checked" /><label for="fullscreen">截取当前桌面</label>
      <input type="radio" name="radioselect" id="specificarea" checked="checked" /><label for="specificarea">截取指定位置</label>
    </div>
    <div id="posdetail" style="position: relative; float:left;padding-left:20px;">
      left:<input class="inputtext" type="input" id="xpos"  value="0"></input>&nbsp;
      top:<input class="inputtext" type="input" id="ypos"  value="0"></input>&nbsp;
      width:<input class="inputtext" type="input" id="width"  value="200"></input>&nbsp;
      height:<input class="inputtext" type="input" id="height"  value="150"></input>
    </div>
  </div>

  <div style="padding-left:20px;"><span id="info"></span></div>
  <div style="padding-left:20px;"><span id="show"></span><a id="btnUpload" href="javascript:UploadData()" class="btn">上传截图</a></div>
  <div id="snapImg" style="height:300px;">
    <img id="imgshow" style="display:none;" border="0" />
  </div>
  <div id="downloadNotice" style="display:none;" >如果控件安装包未自动下载，请&nbsp;<a class="btn" id="downAddr" style="color:#ff0000;" target="_blank" href="./CaptureInstall.exe"><strong>猛戳这里</strong></a>。</div>
  <a id="A1" href="javascript:captureObj.SetWatermarkText('测试水印文字')" class="btn">设置显示水印文字</a>
  <a id="A2" href="javascript:TestSetWatermarkPicture()" class="btn">设置显示水印图片</a>
  <a id="A4" href="javascript:captureObj.SavePicture('')" class="btn">保存刚截图的图片</a>
  <a id="A3" href="javascript:alert(captureObj.GetCursorPosition());" class="btn">获取当前鼠标坐标</a>
  <iframe id="downCapture" style="display:none;"></iframe>

</div>
</template>

<script>
  import $ from 'jquery'
  export default{
    data(){
        return {}
    },
    mounted(){
      $('#moreparams').hide();

      $('#captureselectSize').click( function(){
        var autoFlag = $("#captureselectSize").attr("checked")=="checked" ? 1 : 0;
        if(autoFlag == 1){
          $('#moreparams').show();
        }
        else{
          $('#moreparams').hide();
        }
      });
      $('#getimagefromclipboard').click( function(){
        $('#posdetail').hide();
      });
      $('#showprewindow').click( function(){
        $('#posdetail').hide();
      });
      $('#fullscreen').click( function(){
        $('#posdetail').hide();
      });
      $('#specificarea').click( function(){
        $('#posdetail').show();
      });

      $('#showprewindow').click();
      $('#autoupload').click();
      $('#btnUpload').hide();
      Init();

    }
  }
</script>

<style type="text/css" scoped>
  label{font-size:12px;}
  h3{float:right;margin:4px 30px;line-height:40px;}
  #snapImg{border:1px solid #666;margin-top:10px;height:650px;overflow:auto; text-align:center;}
  .btn{border:1px solid #3079ED;background-color:#498AF4;color:#ffffff;line-height:40px;font-weight:bold; text-decoration:none; text-align:center;padding:5px 20px;}
  .btn:hover{background-color:#3B80EE}
  .inputtext{width:40px;}

</style>
