<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8" %>
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>					
<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt" %>

							<c:if test="${totalcnt eq 0 }">
								<tr>
									<td colspan="5">데이터가 존재하지 않습니다.</td>
								</tr>
							</c:if>
							
							<c:if test="${totalcnt > 0 }">
								<c:forEach items="${accAcmSearchList}" var="list">
									<tr>
										<td>${list.acnt_dt_sbjct_inout}</td>
										<td>${list.acnt_sbject_cd}</td>
										<td>${list.acnt_sbject_name}</td>
										<td>${list.acnt_dt_sbject_cd}</td>
										<td>${list.acnt_dt_sbjct_name}</td>
									</tr>
								</c:forEach>
							</c:if>
							
							<input type="hidden" id="totalcnt" name="totalcnt" value ="${totalcnt}"/>