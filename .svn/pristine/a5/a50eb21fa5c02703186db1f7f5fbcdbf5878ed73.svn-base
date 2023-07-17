<%@ page language="java" contentType="text/html; charset=UTF-8"
	pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge" />
<title>공지사항</title>
<jsp:include page="/WEB-INF/view/common/common_include.jsp"></jsp:include>

<style type="text/css">

	.acv {
			text-align: center;
			border: 0 solid black;
			
			}



</style>

<script type="text/javascript">

	// 페이징 설정
	var pageSize = 10;     
	var pageBlockSize = 5;    
	
	
	
	/** OnLoad event */ 
	$(function() {
		
		// 부서 콤보    상세코드테이블의 상세코드, 상세코드명 으로 만듬   
		comcombo("dep_cd","deptcombo","all","");   // group_code, combo_name, type(기본값  all : 전체   sel : 선택)    , selvalue(선택 되어 나올 값)         
		
		// combo box 종류  acc : 회계 계정     조회 대상 테이블  tb_acnt_sbject   
		selectComCombo("acc","acccombo","all","","");  // combo type(combo box 종류),  combo_name, type(기본값  all : 전체   sel : 선택) , "", "" 
		
		// combo box 종류  accd : 상세 회계계정   acccombo 변경시 계정 상세 재조회 event   조회 대상 테이블  tb_dt_sbject   
		$('#acccombo').change(function() {   
			selectComCombo("accd","accdcombo","all",$('#acccombo').val(),"");  // combo type(combo box 종류),  combo_name, type(기본값  all : 전체   sel : 선택) , 선택된 상위 계정코드, "" 
		});
		
		// combo box 종류  cli : 거래처    조회 대상 테이블  tb_clnt   
		selectComCombo("cli","clicombo","all","","");  // combo type(combo box 종류),  combo_name, type(기본값  all : 전체   sel : 선택) , "", "" 
		
		
		
		// 버튼 이벤트 등록
		fRegisterButtonClickEvent();
		
		fn_acSearchlist();
		
		
		
		
	});
	

	/** 버튼 이벤트 등록 */

	function fRegisterButtonClickEvent() {
		$('a[name=btn]').click(function(e) {
			e.preventDefault();

			var btnId = $(this).attr('id');

			switch (btnId) {
				case 'btnSearch' :
					fn_acSearchlist();
					break;
				case 'btnSave' :
					fn_save();
					break;	
				case 'btnDelete' :
					$("#action").val("D");	
					fn_save();
					break;	
				case 'btnDeleteFile' :
					$("#action").val("D");	
					fn_savefile();
					break;		
				case 'btnSaveFile' :
					fn_savefile();
					break;	
				case 'btnClose' :
				case 'btnCloseFile' :
					gfCloseModal();
					break;
			}
		});
	}
	
	
	function fn_acSearchlist(pagenum) {
		
		pagenum = pagenum || 1;
		
		var param = {
		    start : $("#start").val()
		  , end : $("#end").val()
		  , clicombo : $("#clicombo").val()
		  ,	acccombo : $("#acccombo").val()
		  , accdcombo : $("#accdcombo").val()
		  , pageSize : pageSize
		  , pageBlockSize : pageBlockSize
		  , pagenum : pagenum
		}
		
		var listcollabck = function(returnvalue) {
			console.log(returnvalue);
			
			$("#acSearchlist").empty().append(returnvalue);
			
			var  totalcnt = $("#totalcnt").val();
			
			console.log("totalcnt : " + totalcnt);
			
			var paginationHtml = getPaginationHtml(pagenum, totalcnt, pageSize, pageBlockSize, 'fn_acSearchlist');
			console.log("paginationHtml : " + paginationHtml);
			 
			$("#acSearchlistPagination").empty().append( paginationHtml );
			
			$("#pageno").val(pagenum);
		}
		
		callAjax("/accAcs/accountSearchList.do", "post", "text", false, param, listcollabck) ;
			
	}
	
	function fn_openpopup() {
		
		popupinit();
		
		// 모달 팝업
		gfModalPop("#layer1");
		
		
	}
	
	function popupinit(object) {
		
		if(object == "" || object == null || object == undefined) {
// 			$("#bno").val("");		
// 			$("#notice_cont").val("");
// 			$("#notice_no").val("");
			
// 			$("#btnDelete").hide();
			
// 			$("#action").val("I");	
		} else {
			$("#bno").val(object.budget_no);		
			$("#person").val(object.name);
			$("#date").val(object.pdate);
			
			if(JSON.stringify(object.order_no) ==  0){
				
				$("#Ono").val("");
			} else
			
			$("#Ono").val(object.order_no);
			
			if(object.dlv_no == 0){
				
				$("#Dno").val("");
			} else
			$("#Dno").val(object.dlv_no);

			if(object.expen_report_no == 0){
				
				$("#Eno").val("");
			} else
			
			$("#Eno").val(object.expen_report_no);
			$("#Suname1").val(object.acnt_dt_sbjct_name);
			$("#E1").val(object.outamt);
			$("#R1").val(object.inamt);
			
			
			
			$("#TE").val(object.outamt);
			$("#TR").val(object.inamt);
			
// 			$("#btnDelete").show();
			
		}
	}
	
	function fn_selectone(no) {
		
		//alert(no);
		
		var param = {
				budget_no : no
		}
		
		var selectoncallback = function(returndata) {			
			console.log( JSON.stringify(returndata) );
								
			popupinit(returndata.accountSearchSelectone);
			
			// 모달 팝업
			gfModalPop("#layer1");
			
		}
		
		callAjax("/accAcs/accountSearchSelectone.do", "post", "json", false, param, selectoncallback) ;
		
	}
	
	function fn_save() {
		
		if ( ! fn_Validate() ) {
			return;
		}
		
		var param = {
				action : $("#action").val(),
				notice_no : $("#notice_no").val(),
				notice_title : $("#notice_title").val(),
				notice_cont : $("#notice_cont").val()
		}
		
		var savecollback = function(reval) {
			console.log( JSON.stringify(reval) );
			
			if(reval.returncval > 0) {
				alert("저장 되었습니다.");
				gfCloseModal();
				
				if($("#action").val() == "U") {
					fn_noticelist($("#pageno").val());
				} else {
					fn_noticelist();
				}
			}  else {
				alert("오류가 발생 되었습니다.");				
			}
		}
		
		//callAjax("/mngNot/noticesave.do", "post", "json", false, param, savecollback) ;
		callAjax("/mngNot/noticesave.do", "post", "json", false, $("#myForm").serialize() , savecollback) ;
		
	}
	
	function fn_Validate() {

		var chk = checkNotEmpty(
				[
						[ "notice_title", "제목을 입력해 주세요." ]
					,	[ "notice_cont", "내용을 입력해 주세요" ]
				]
		);

		if (!chk) {
			return;
		}

		return true;
	}
	
	//////////////////////////   위는 파일 업이 처리
	/////////////////////////    file upload
	
	function fn_openpopupfile() {
        popupinitfile();
		
		// 모달 팝업
		gfModalPop("#layer2");
	}
	
   function popupinitfile(object) {
		
		if(object == "" || object == null || object == undefined) {
// 			$("#bno").val("");		
// 			$("#file_notice_cont").val("");
// 			$("#notice_no").val("");
// 			$("#upfile").val("");		
			
// 			$("#previewdiv").empty();
			
// 			$("#btnDeleteFile").hide();
			
// 			$("#action").val("I");	
		} else {

			$("#bno").val(object.budget_no);		
			$("#file_notice_cont").val(object.notice_cont);
			$("#notice_no").val(object.notice_no);
			$("#upfile").val("");		
			
			var inserthtml = "<a href='javascript:fn_filedownload()'>";
			
			if(object.file_name == "" || object.file_name == null || object.file_name == undefined) {
				inserthtml += "";
			} else {
				var selfile = object.file_name;
			    var selfilearr = selfile.split(".");
			    var lastindex = selfilearr.length - 1;
			    if(selfilearr[lastindex].toLowerCase() == "jpg" || selfilearr[lastindex].toLowerCase() == "gif" || selfilearr[lastindex].toLowerCase() == "jpge" || selfilearr[lastindex].toLowerCase() == "png") {
			    	  inserthtml += "<img src='" + object.logic_path + "' style='width:100px; height:80px' />";
			    } else {
			    	  inserthtml += object.file_name;
			    }				
			} 
			

			inserthtml += "</a>"
			
			$("#previewdiv").empty().append(inserthtml);
			
			$("#btnDeleteFile").show();
			
			$("#action").val("U");	
		}
	}
	
	function preview(event) {
		var image = event.target;
		  
		//alert(image.files[0].file_name + " : " + image.files[0].file_nm + " : " + image.files[0].name);
		
		 if(image.files[0]){
			  //alert(window.URL.createObjectURL(image.files[0]));
			 
			  var selfile = image.files[0].name;
		      var selfilearr = selfile.split(".");
		      var inserthtml = "";
		      var lastindex = selfilearr.length - 1;
		      
		      
		      if(selfilearr[lastindex].toLowerCase() == "jpg" || selfilearr[lastindex].toLowerCase() == "gif" || selfilearr[lastindex].toLowerCase() == "jpge" || selfilearr[lastindex].toLowerCase() == "png") {
		    	  inserthtml = "<img src='" + window.URL.createObjectURL(image.files[0]) + "' style='width:100px; height:80px' />";
		      } else {
		    	  inserthtml = selfile;
		      }
			  
			  
			  $("#previewdiv").empty().append(inserthtml);
		}
		
		
	}
	
	function fn_savefile() {
		
		var frm = document.getElementById("myForm");
		frm.enctype = 'multipart/form-data';
		var fileData = new FormData(frm);
		
		var filesavecallback = function(returnval) {
			console.log( JSON.stringify(returnval) );
			
			if(returnval.returncval > 0) {
				alert("저장 되었습니다.");
				gfCloseModal();
				
				if($("#action").val() == "U") {
					fn_noticelist($("#pageno").val());
				} else {
					fn_noticelist();
				}
			}  else {
				alert("오류가 발생 되었습니다.");				
			}
		}
				
		callAjaxFileUploadSetFormData("/mngNot/noticesavefile.do", "post", "json", true, fileData, filesavecallback);
		
	}
	
	function fn_selectonefile(no) {
		
		//alert(no);
		
		var param = {
				notice_no : no
		}
		
		var selectoncallback = function(returndata) {			
			console.log( JSON.stringify(returndata) );
								
			popupinitfile(returndata.noticesearch);
			
			// 모달 팝업
			gfModalPop("#layer2");
			
		}
		
		callAjax("/mngNot/noticeselectone.do", "post", "json", false, param, selectoncallback) ;
		
	}
	
	function fn_filedownload() {
		alert("다운로드");
		
		var params = "";
		params += "<input type='hidden' name='notice_no' id='notice_no' value='"+ $("#notice_no").val() +"' />";
		
		jQuery("<form action='/mngNot/downloadnoticefile.do' method='post'>"+params+"</form>").appendTo('body').submit().remove();
		
	}
	
	
	
	
	
	
	
</script>

</head>
<body>
<form id="myForm" action=""  method="">
	<input type="hidden" id="action"  name="action"  />
	<input type="hidden" id="notice_no"  name="notice_no"  />
	<input type="hidden" id="pageno"  name="pageno"  />
	
	<!-- 모달 배경 -->
	<div id="mask"></div>

	<div id="wrap_area">

		<h2 class="hidden">header 영역</h2>
		<jsp:include page="/WEB-INF/view/common/header.jsp"></jsp:include>

		<h2 class="hidden">컨텐츠 영역</h2>
		<div id="container">
			<ul>
				<li class="lnb">
					<!-- lnb 영역 --> <jsp:include
						page="/WEB-INF/view/common/lnbMenu.jsp"></jsp:include> <!--// lnb 영역 -->
				</li>
				<li class="contents">
					<!-- contents -->
					<h3 class="hidden">contents 영역</h3> <!-- content -->
					<div class="content">

						<p class="Location">
							<a href="../dashboard/dashboard.do" class="btn_set home">메인으로</a> <span
								class="btn_nav bold">운영</span> <span class="btn_nav bold">공지사항
								관리</span> <a href="../system/comnCodMgr.do" class="btn_set refresh">새로고침</a>
						</p>
                        
                        
                        
                        
						<p class="conTitle">
							<span>회계전표</span> <span class="fr"> 
						</p>
						
						
							<label for="start" style="font-size: 15px;">기간 조회 : </label>
							<input type="date" id="start" name="start" min="2023-01-01" style="height: 25px; width: 100px;">
							<span> ~ </span>
							<input type="date" id="end" name="end" min="2023-01-01" style="height: 25px; width: 100px;">
							
							<label for="clicombo" style="margin-left: 15px; font-size: 15px;">거래처명 : </label>
							<select id="clicombo" name="clicombo" style="height: 25px; width: 120px;" >
							</select> 
							
							<label for="acccombo" style="margin-left: 15px; font-size: 15px;">계정 대분류 : </label>
							<select id="acccombo" name="acccombo" style="height: 25px; width: 100px;">
							        <option value="" >전체</option>
							</select> 
							
							<label for="accdcombo" style="margin-left: 15px; font-size: 15px;">계정 상세 : </label>
							 <select id="accdcombo" name="accdcombo" style="width: 100px;" >
							        <option value="" >전체</option>
									<option value="1000" >상품매출</option>
									<option value="2000" >상품매입</option>
									<option value="3000" >직원급여</option>
									<option value="4000" >퇴직급여</option>
									<option value="5000" >보험료</option>
									<option value="6000" >소모품비</option>
									<option value="7000" >여비교통비</option>
									<option value="8000" >법인세</option>
							</select> 
							<a href="" class="btnType blue" id="btnSearch" name="btn" style="margin-left: 30px;"><span>검  색</span></a>
<!-- 							 <a class="btnType blue" href="javascript:fn_openpopup();" name="modal"><span>신규등록</span></a> -->
<!-- 							 <a class="btnType blue" href="javascript:fn_openpopupfile();" name="modal"><span>신규등록 파일</span></a> -->
							</span>
						<p style="margin-bottom: 10px;"></p>
						
						<div class="acSearchlist">
							<table class="col">
								<caption>caption</caption>
								<colgroup>
									<col width="5%">
									<col width="15%">
									<col width="10%">
									<col width="15%">
									<col width="15%">
									<col width="20%">
									<col width="20%">
								</colgroup>
	
								<thead>
									<tr>
										<th scope="col">번호</th>
										<th scope="col">날짜</th>
										<th scope="col">구분</th>
										<th scope="col">계정과목</th>
										<th scope="col">거래처</th>
										<th scope="col">비용</th>
										<th scope="col">수익</th>
									</tr>
								</thead>
								<tbody id="acSearchlist"></tbody>
							</table>
						</div>
	
						<div class="paging_area"  id="acSearchlistPagination"> </div>
						

					</div> <!--// content -->

					<h3 class="hidden">풋터 영역</h3>
						<jsp:include page="/WEB-INF/view/common/footer.jsp"></jsp:include>
				</li>
			</ul>
		</div>
	</div>

	<!-- 모달팝업 -->
	<div id="layer1" class="layerPop layerType2" style="width: 900px; height: 500px;">
		<dl>
			<dt>
				<strong>회계전표 상세</strong>
			</dt>
			<dd class="content">
				<!-- s : 여기에 내용입력 -->
				<table class="row">
					<caption>caption</caption>
					<colgroup>
						<col width="120px">
						<col width="*">
						<col width="120px">
						<col width="*">
					</colgroup>

					<tbody>
						<tr>
							<th scope="row">전표번호</th>
							<td colspan="3"><input type="text" class="inputTxt p100 acv" name="bno" id="bno" style="border:none"/></td>
							<th scope="row">담당자</th>
							<td colspan="3"><input type="text" class="inputTxt p100 acv" name="person" id="person" style="border:none"/></td>
							<th scope="row">일자</th>
							<td colspan="3"><input type="text" class="inputTxt p100 acv" name="date" id="date" style="border:none" /></td>
						</tr>
						<tr>
							<th scope="row">주문번호</th>
							<td colspan="3"><input type="text" class="inputTxt p100 acv" name="Ono" id="Ono" style="border:none"/></td>
							<th scope="row">발주번호</th>
							<td colspan="3"><input type="text" class="inputTxt p100 acv" name="Dno" id="Dno" style="border:none"/></td>
							<th scope="row">지출번호</th>
							<td colspan="3"><input type="text" class="inputTxt p100 acv" name="Eno" id="Eno" style="border:none"/></td>
						</tr>
						
						<tr>
							<th scope="row" colspan="4">계정과목</th>
							<th scope="row" colspan="4">비용</th>
							<th scope="row" colspan="4">수익</th>
							
						</tr>
						<tr>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="Suname1" id="Suname1" style="border:none"/></td>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="E1" id="E1" style="border:none"/></td>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="R1" id="R1" style="border:none"/></td>
						</tr>
						<tr>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="Suname2" id="Suname2" style="border:none"/></td>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="E2" id="E2" style="border:none"/></td>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="R2" id="R2" style="border:none"/></td>
						</tr>
						<tr>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="Suname3" id="Suname3" style="border:none"/></td>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="E3" id="E3" style="border:none"/></td>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="R3" id="R3" style="border:none"/></td>
						</tr>
						<tr>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="Suname4" id="Suname4" style="border:none"/></td>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="E4" id="E4" style="border:none"/></td>
							<td colspan="4"><input type="text" class="inputTxt p100 acv" name="R4" id="R4" style="border:none" /></td>
						</tr>
						<tr>
							<th scope="row" colspan="4">합계</th>
							<th colspan="4"><input type="text" class="inputTxt p100 acv" name="TE" id="TE" style="border:none; background: #bbc2cd; font-weight: bold;" /></th>
							<th colspan="4"><input type="text" class="inputTxt p100 acv" name="TR" id="TR" style="border:none; background: #bbc2cd; font-weight: bold;" /></th>
						</tr>
					</tbody>
				</table>

				<!-- e : 여기에 내용입력 -->

<!-- 				<div class="btn_areaC mt30"> -->
<!-- 					<a href="" class="btnType blue" id="btnSave" name="btn"><span>저장</span></a>  -->
<!-- 					<a href="" class="btnType blue" id="btnDelete" name="btn"><span>삭제</span></a>  -->
					
					<a href=""	class="btnType gray"  id="btnClose" name="btn" style="margin-left: 45.5%; margin-top: 30px; "><span>닫기</span></a>
<!-- 				</div> -->
			</dd>
		</dl>
		<a href="" class="closePop"><span class="hidden">닫기</span></a>
	</div>

	<div id="layer2" class="layerPop layerType2" style="width: 600px;">
		<dl>
			<dt>
				<strong>상세코드 관리</strong>
			</dt>
			<dd class="content">

				<!-- s : 여기에 내용입력 -->

				<table class="row">
					<caption>caption</caption>
					<colgroup>
						<col width="120px">
						<col width="*">
						<col width="120px">
						<col width="*">
					</colgroup>

					<tbody>
						<tr>
							<th scope="row">제목 <span class="font_red">*</span></th>
							<td colspan="3"><input type="text" class="inputTxt p100" name="file_notice_title" id="file_notice_title" /></td>
						</tr>
						<tr>
							<th scope="row">내용 <span class="font_red">*</span></th>
							<td colspan="3">
							    <textarea id="file_notice_cont" name="file_notice_cont"> </textarea>
							</td>
						</tr>
				        <tr>
							<td colspan=2>
							    <input type="file" id="upfile"  name="upfile"  onchange="javascript:preview(event)" />
							</td>
							<td colspan=2>
							      <div id="previewdiv" ></div>
							</td>
						</tr>
					</tbody>
				</table>

				<!-- e : 여기에 내용입력 -->

				<div class="btn_areaC mt30">
					<a href="" class="btnType blue" id="btnSaveFile" name="btn"><span>저장</span></a>
					<a href="" class="btnType blue" id="btnDeleteFile" name="btn"><span>삭제</span></a>  
					<a href="" class="btnType gray" id="btnCloseFile" name="btn"><span>취소</span></a>
				</div>
			</dd>
		</dl>
		<a href="" class="closePop"><span class="hidden">닫기</span></a>
	</div>
	<!--// 모달팝업 -->
</form>
</body>
</html>