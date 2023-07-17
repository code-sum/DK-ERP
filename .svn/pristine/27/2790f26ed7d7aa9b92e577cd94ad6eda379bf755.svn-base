<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8"%>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <title>인사관리</title>
  <jsp:include page="/WEB-INF/view/common/common_include.jsp"></jsp:include>

  <script type="text/javascript">

    // 페이징 설정
    var pageSize = 10;
    var pageBlockSize = 5;



    /** OnLoad event */
    $(function() {
      // 버튼 이벤트 등록
      fRegisterButtonClickEvent();

      fn_emplist();


    });


    /** 버튼 이벤트 등록 */

    function fRegisterButtonClickEvent() {
      $('a[name=btn]').click(function(e) {
        e.preventDefault();

        var btnId = $(this).attr('id');

        switch (btnId) {
          case 'btnSearch' :
            fn_emplist();
            break;
          case 'btnSave' :
            fn_save();
            break;
          case 'btnDelete' :
            $("#action").val("D");
            fn_save();
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


    function fn_emplist(pagenum) {

      pagenum = pagenum || 1;

      var param = {
        deptcd : $("#deptcd").val()
        ,   lvcd : $("#lvcd").val()
        ,	searchKey : $("#searchKey").val()
        , 	ename : $("#ename").val()
        , pageSize : pageSize
        , pageBlockSize : pageBlockSize
        , pagenum : pagenum
      }

      var listcollabck = function(returnvalue) {
        console.log(returnvalue);

        $("#listemp").empty().append(returnvalue);

        var  totalcnt = $("#totalcnt").val();

        console.log("totalcnt : " + totalcnt);

        var paginationHtml = getPaginationHtml(pagenum, totalcnt, pageSize, pageBlockSize, 'fn_emplist');
        console.log("paginationHtml : " + paginationHtml);

        $("#empPagination").empty().append( paginationHtml );

        $("#pageno").val(pagenum);
      }

      callAjax("/empEpm/emplist.do", "post", "text", false, param, listcollabck) ;

    }

    function fn_openpopup() {

      popupinit();

      // 모달 팝업
      gfModalPop("#layer1");


    }

    function popupinit(object) {

      if(object == "" || object == null || object == undefined) {

        $("#emp_birth").val("");
        $("#name").val("");
        $("#emp_sex").val("");
        $("#emp_edu").val("");
        $("#emp_email").val("");
        $("#emp_hp").val("");
        $("#emp_zip").val("");
        $("#emp_addr").val("");
        $("#emp_dt_addr").val("");
        $("#bk_cd").val("");
        $("#emp_account").val("");
        $("#dept_cd").val("");
        $("#level_cd").val("");
        $("#emp_yr_sal").val("");
        $("#emp_sdate").val("");
        $("#emp_edate").val("");
        $("#retire_reason").val("");


        $("#btnDelete").hide();

        $("#action").val("I");
      } else {

        $("#emp_birth").val(object.emp_birth);
        $("#name").val(object.name);
        $("#emp_sex").val(object.emp_sex);
        $("#emp_edu").val(object.emp_edu);
        $("#emp_email").val(object.emp_email);
        $("#emp_hp").val(object.emp_hp);
        $("#emp_zip").val(object.emp_zip);
        $("#emp_addr").val(object.emp_addr);
        $("#emp_dt_addr").val(object.emp_dt_addr);
        $("#bk_cd").val(object.bk_cd);
        $("#emp_account").val(object.emp_account);
        $("#dept_cd").val(object.dept_cd);
        $("#level_cd").val(object.level_cd);
        $("#emp_yr_sal").val(object.emp_yr_sal);
        $("#emp_sdate").val(object.emp_sdate);
        $("#emp_edate").val(object.emp_edate);
        $("#retire_reason").val(object.retire_reason);



        $("#btnDelete").show();

        $("#action").val("U");
      }
    }

    function fn_empSelectOne(login) {

      //alert(no);

      var param = {
        loginId : login
      }

      var selectoncallback = function(returndata) {
        console.log( JSON.stringify(returndata) );

        popupinit(returndata.empSearch);

        // 모달 팝업
        gfModalPop("#layer1");

      }

      callAjax("/empEpm/empSelectOne.do", "post", "json", false, param, selectoncallback) ;

    }

    function fn_save() {

      if ( ! fn_Validate() ) {
        return;
      }

      /*
      var param = {
        action : $("#id").val(),
        loginId : $("#loginId").val(""),
        emp_birth : $("#emp_birth").val(""),
        name : $("#name").val(""),
        emp_sex : $("#emp_sex").val(""),
        emp_edu : $("#emp_edu").val(""),
        emp_email : $("#emp_email").val(""),
        emp_hp : $("#emp_hp").val(""),
        emp_zip : $("#emp_zip").val(""),
        emp_dt_addr : $("#emp_dt_addr").val(""),
        bk_cd : $("#bk_cd").val(""),
        emp_account : $("#emp_account").val(""),
        dept_cd : $("#dept_cd").val(""),
        level_cd : $("#level_cd").val(""),
        emp_yr_sal : $("#emp_yr_sal").val(""),
        emp_sdate : $("#emp_sdate").val(""),
        emp_edate : $("#emp_edate").val(""),
        sal_date : $("#sal_date").val(""),
        retire_reason : $("#retire_reason").val(""),
        emp_addr : $("#emp_addr").val(""),
        emp_work_yn : $("#emp_work_yn").val(""),
        sal_san : $("#sal_san").val(""),
        retire_reason : $("#retire_reason").val(""),
        sal_ko : $("#sal_ko").val(""),
        sal_kun : $("#sal_kun").val(""),
        sal_kuk : $("#sal_kuk").val(""),
        sal_pre : $("#sal_pre").val(""),
        sal_after : $("#sal_after").val("")


      }
      */


      var savecollback = function(reval) {
        console.log( JSON.stringify(reval) );

        if(reval.returncval > 0) {
          alert("저장 되었습니다.");
          gfCloseModal();

          if($("#action").val() == "U") {
            fn_emplist($("#pageno").val());
          } else {
            fn_emplist();
          }
        }  else {
          alert("오류가 발생 되었습니다.");
        }
      }


      callAjax("/empEpm/empSave.do", "post", "json", false, $("#myForm").serialize() , savecollback) ;

    }
    function fn_Validate() {
      var chk = checkNotEmpty(
              [
                [ "emp_birth", "생일을 입력해 주세요." ]
                ,	[ "name", "이름을 입력해 주세요." ]
                ,	[ "emp_sex", "성별을 입력해 주세요." ]
                ,	[ "emp_edu", "학력을 입력해 주세요." ]
                ,	[ "emp_email", "이메일을 입력해 주세요." ]
                ,	[ "emp_hp", "전화번호를 선택해 주세요." ]

              ]
      );
      if (!chk) {
        return;
      }
      return true;
    }



    //////////////////////////   위는 파일 업이 처리
    /////////////////////////    file upload













  </script>

</head>
<body>
<form id="myForm" action=""  method="">
  <input type="hidden" id="action"  name="action"  />
  <input type="hidden" id="loginId"  name="loginId"  />
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
              <span>인사관리</span> <span class="fr">
							<select id="deptcd" name="deptcd" style="width: 150px;">
							        <option value="" >전체</option>
									<option value="100" >관리자</option>
									<option value="200" >임원직</option>
                                    <option value="300" >회계팀</option>
                                    <option value="400" >영업팀</option>
                                    <option value="500" >인사팀</option>
							</select>

                            <select id="lvcd" name="lvcd" style="width: 150px;">
							        <option value="" >전체</option>
									<option value="10" >사원</option>
									<option value="20" >주임</option>
                                    <option value="30" >대리</option>
                                    <option value="40" >과장</option>
                                    <option value="50" >부장</option>
                                    <option value="60" >상무</option>
                                    <option value="70" >전무</option>
                                    <option value="80" >이사</option>
                                    <option value="90" >대표</option>
							</select>
							 <select id="searchKey" name="searchKey" style="width: 150px;" >
							        <option value="" >전체</option>
									<option value="loginId" >사번</option>
									<option value="name" >사원명</option>
							</select>
							<input type="text" style="width: 300px; height: 25px;" id="ename" name="ename">
							<a href="" class="btnType blue" id="btnSearch" name="btn"><span>검  색</span></a>
							 <a class="btnType blue" href="javascript:fn_openpopup();" name="modal"><span>신규등록</span></a>

							</span>
            </p>

            <div class="empList">
              <table class="col">
                <caption>caption</caption>
                <colgroup>
                  <col width="10%">
                  <col width="30%">
                  <col width="10%">
                  <col width="10%">
                  <col width="15%">
                  <col width="10%">
                  <col width="10%">
                  <col width="5%">
                </colgroup>

                <thead>
                <tr>
                  <th scope="col">사번</th>
                  <th scope="col">이름</th>
                  <th scope="col">부서코드</th>
                  <th scope="col">부서명</th>
                  <th scope="col">직급</th>
                  <th scope="col">입사일자</th>
                  <th scope="col">재직구분</th>
                  <th scope="col">상세</th>
                </tr>
                </thead>
                <tbody id="listemp"></tbody>
              </table>
            </div>

            <div class="paging_area"  id="empPagination"> </div>


          </div> <!--// content -->

          <h3 class="hidden">풋터 영역</h3>
          <jsp:include page="/WEB-INF/view/common/footer.jsp"></jsp:include>
        </li>
      </ul>
    </div>
  </div>

  <!-- 모달팝업 -->
  <div id="layer1" class="layerPop layerType2" style="width: 600px;">
    <dl>
      <dt>
        <strong>그룹코드 관리</strong>
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

            <th scope="row">생년월일 <span class="font_red">*</span></th>
            <td><input type="text" class="inputTxt p100" name="emp_birth" id="emp_birth" /></td>
          </tr>
          <tr>
            <th scope="row">이름 <span class="font_red">*</span></th>
            <td><input type="text" class="inputTxt p100" name="name" id="name" /></td>
            <th scope="row">성별 <span class="font_red">*</span></th>
            <td><input type="text" class="inputTxt p100" name="emp_sex" id="emp_sex" /></td>
          </tr>
          <tr>
            <th scope="row">학력 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="emp_edu" id="emp_edu" /></td>
          </tr>
          <tr>
            <th scope="row">이메일 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="emp_email" id="emp_email" /></td>
          </tr>
          <tr>
            <th scope="row">전화번호 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="emp_hp" id="emp_hp" /></td>
          </tr>
          <tr>
            <th scope="row">우편번호 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="emp_zip" id="emp_zip" /></td>
          </tr>
          <tr>
            <th scope="row">주소 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="emp_addr" id="emp_addr" /></td>
          </tr>
          <tr>
            <th scope="row">상세주소 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="emp_dt_addr" id="emp_dt_addr" /></td>
          </tr>
          <tr>
            <th scope="row">은행 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="bk_cd" id="bk_cd" /></td>
          </tr>
          <tr>
            <th scope="row">계좌번호 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="emp_account" id="emp_account" /></td>
          </tr>
          <tr>
            <th scope="row">부서 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="dept_cd" id="dept_cd" /></td>
          </tr>
          <tr>
            <th scope="row">직급 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="level_cd" id="level_cd" /></td>
          </tr>
          <tr>
            <th scope="row">연봉 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="emp_yr_sal" id="emp_yr_sal" /></td>
          </tr>
          <tr>
            <th scope="row">입사일 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="emp_sdate" id="emp_sdate" /></td>
          </tr>
          <tr>
            <th scope="row">퇴사일 <span class="font_red">*</span></th>
            <td colspan="3"><input type="text" class="inputTxt p100" name="emp_edate" id="emp_edate" /></td>
          </tr>
          <tr>
            <th scope="row">퇴사내용 </th>
            <td colspan="3">
              <textarea id="retire_reason" name="retire_reason"> </textarea>
            </td>
          </tr>
          </tbody>
        </table>

        <!-- e : 여기에 내용입력 -->

        <div class="btn_areaC mt30">
          <a href="" class="btnType blue" id="btnSave" name="btn"><span>저장</span></a>
          <a href="" class="btnType blue" id="btnDelete" name="btn"><span>삭제</span></a>
          <a href=""	class="btnType gray"  id="btnClose" name="btn"><span>취소</span></a>
        </div>
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
