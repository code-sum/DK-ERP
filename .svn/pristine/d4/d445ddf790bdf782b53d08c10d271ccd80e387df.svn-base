<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>					
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>

							<c:if test="${totalcnt eq 0 }">
								<tr>
									<td colspan="15">데이터가 존재하지 않습니다.</td>
								</tr>
							</c:if>
							
							<c:if test="${totalcnt > 0 }">
								<c:forEach items="${empSamSearchList}" var="list">
									<tr>
										<td>${list.sal_date}</td>
										<td>${list.loginID}</td>
										<td>${list.name}</td>
										<td>${list.dept_name}</td>
										<td>${list.level_name}</td>
										<td>${list.emp_yr_sal}</td>
										<td>${list.sal_pre}</td>
										<td>${list.sal_san}</td>
										<td>${list.sal_ko}</td>
										<td>${list.sal_kun}</td>
										<td>${list.sal_kuk}</td>
										<td>${list.sal_after}</td>
										<td>${list.emp_final_money}</td>
										<td>${list.emp_meno}</td>
									<c:if test="${list.sal_pay_yn eq 'N'}">
										<td><a class="btnType2 color2" href="javascript:fn_openpopup(${list.loginID}, ${list.sal_date.substring(0,4).concat(list.sal_date.substring(5))});" id="btnChoice" name="modal"  >미지급</a></td>
									</c:if>
									<c:if test="${list.sal_pay_yn eq 'Y'}">
										<td><a class="btnType2 color2" id="btnChoice" name="modal" >지급</a></td>
									</c:if>
										
									</tr>
								</c:forEach>
							</c:if>
							
							<input type="hidden" id="totalcnt" name="totalcnt" value ="${totalcnt}"/>
							