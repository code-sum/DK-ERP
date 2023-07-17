<%@ page language="java" contentType="text/html; charset=UTF-8"
         pageEncoding="UTF-8" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>

<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge"/>
    <title>일별 매출 현황</title>
    <jsp:include page="/WEB-INF/view/common/common_include.jsp"></jsp:include>

    <script type="text/javascript">

        // 페이징 설정
        var pageSize = 5;
        var pageBlockSize = 5;


        /** OnLoad event */
        $(function () {
            // 버튼 이벤트 등록
            fRegisterButtonClickEvent();

            fn_saleDayList();

        });


        /** 버튼 이벤트 등록 */
        function fRegisterButtonClickEvent() {
            $('a[name=btn]').click(function (e) {
                e.preventDefault();

                var btnId = $(this).attr('id');

                switch (btnId) {
                    case 'btnSearch' :
                        fn_saleDayList();
                        break;
                }
            });
        }

        function fn_saleDayList(pagenum) {
            pagenum = pagenum || 1;

            var param = {
                selectedValue: $("#proName").val(),
                selectedValue: $("#splrName").val(),
                searchKey: $("#searchKey").val(),
                selectedValue: $("#pname").val(),
                pageSize: pageSize,
                pageBlockSize: pageBlockSize,
                pagenum: pagenum
            };


            var listCallBack = function (returnValue) {
                console.log(returnValue);

                $("#listSaleDay").empty().append(returnValue);

                var totalCnt = $("#totalCnt").val();

                console.log("totalCnt: " + totalCnt);

                var paginationHtml = getPaginationHtml(pagenum, totalCnt, pageSize, pageBlockSize, 'fn_saleDayList');
                console.log("paginationHtml: " + paginationHtml);

                $("#saleDayPagination").empty().append(paginationHtml);

                $("#pageno").val(pagenum);
            };

            callAjax("/selSaD/saleDayList.do", "post", "text", false, param, listCallBack);
        }


    </script>

</head>
<body>
<form id="myForm" action="" method="">
    <input type="hidden" id="action" name="action"/>
    <input type="hidden" id="order_no" name="order_no"/>
    <input type="hidden" id="pageno" name="pageno"/>

    <!-- 모달 배경 -->
    <div id="mask"></div>

    <div id="wrap_area">

        <h2 class="hidden">header 영역</h2>
        <jsp:include page="/WEB-INF/view/common/header.jsp"></jsp:include>

        <h2 class="hidden">컨텐츠 영역</h2>
        <div id="container">
            <ul>
                <li class="lnb">
                    <!-- lnb 영역 -->
                    <jsp:include
                            page="/WEB-INF/view/common/lnbMenu.jsp"></jsp:include> <!--// lnb 영역 -->
                </li>
                <li class="contents">
                    <!-- contents -->
                    <h3 class="hidden">contents 영역</h3> <!-- content -->
                    <div class="content">

                        <p class="Location">
                            <a href="../dashboard/dashboard.do" class="btn_set home">메인으로</a> <span
                                class="btn_nav bold">매출</span> <span class="btn_nav bold">일별 매출 현황
								</span> <a href="../selSaD/saleDay.do" class="btn_set refresh">새로고침</a>
                        </p>


                        <p class="conTitle">
                            <span>일별 매출 현황</span> <span class="fr">
					</span>
                        </p>

                        <!-- 검색창 영역 시작 -->

                        <div style="display:flex; justify-content:center; align-content:center; border:1px solid DeepSkyBlue; padding:10px 10px; margin-bottom: 8px;">
                            <label for="start" style="font-size: 15px; margin-right:5px; ">기간 조회 : </label>
                            <input type="date" id="start" name="start" min="2023-01-01"
                                   style="height: 25px; width: 120px;">
                            <label for="clicombo" style="margin-left: 15px; font-size: 15px;">거래처명 : </label>
                            <select id="clicombo" name="clicombo" style="height: 25px; width: 120px;">
                            </select>

                            <label for="acccombo" style="margin-left: 15px; font-size: 15px;">계정 대분류 : </label>
                            <select id="acccombo" name="acccombo" style="height: 25px; width: 100px;">
                                <option value="">전체</option>
                            </select>

                            </select>
                            <input type="text" style="width: 200px; height: 25px; margin-right:5px; " id="pname"
                                   name="pname">
                            <a href="" class="btnType blue" id="btnSearch" name="btn"><span>검  색</span></a>
                            </p>
                        </div>
                        <!-- 검색창 영역 끝 -->


                        <div class="saleDayList">


                            <style>
                                table {
                                    width: 100%;
                                    border-collapse: collapse;
                                }

                                th, td {
                                    text-align: center;
                                    padding: 5px;
                                    border: 1px solid black;
                                }
                            </style>
                            <table class="col">
                                <caption>caption</caption>
                                <tr>
                                    <th>매출</th>

                                    <td>${tem_in1}</td>
                                </tr>
                                <tr>
                                    <th>매출 원가</th>

                                    <td>${tem_in2}</td>
                                </tr>
                                <tr>

                                    <th>매출 순이익</th>
                                    <td>${tem_in3}</td>
                                </tr>
                                <tr>

                                    <th>매출 이익률</th>
                                    <td>${tem_in4}</td>
                                </tr>
                            </table>


                            <table class="col">
                                <caption>caption</caption>
                                <colgroup>
                                    <col width="12%">
                                    <col width="5%">
                                    <col width="9%">
                                    <col width="9%">
                                    <col width="9%">
                                    <col width="12%">
                                    <col width="9%">
                                    <col width="9%">
                                    <col width="9%">
                                    <col width="5%">
                                    <col width="9%">
                                </colgroup>

                                <thead>
                                <tr>
                                    <th scope="col">주문 일자</th>
                                    <th scope="col">주문 번호</th>
                                    <th scope="col">고객기업명</th>
                                    <th scope="col">제품 분류</th>
                                    <th scope="col">제조사</th>
                                    <th scope="col">품명</th>
                                    <th scope="col">모델명</th>
                                    <th scope="col">납품단가</th>
                                    <th scope="col">판매가</th>
                                    <th scope="col">수량</th>
                                    <th scope="col">총액</th>

                                </tr>
                                </thead>
                                <tbody id="listSaleDay"></tbody>
                            </table>
                        </div>

                        <div class="paging_area" id="saleDayPagination"></div>


                    </div> <!--// content -->

                    <h3 class="hidden">풋터 영역</h3>
                    <jsp:include page="/WEB-INF/view/common/footer.jsp"></jsp:include>
                </li>
            </ul>
        </div>
    </div>


</form>
</body>
</html>