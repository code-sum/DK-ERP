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
								<c:forEach items="${accountSearchList}" var="list">
									<tr>
										<td>${list.budget_no}</a></td>
										<td><a href="javascript:fn_selectone('${list.budget_no}')">${list.pdate}</a></td>
										<td>${list.acnt_dt_sbjct_inout}</td>
										<td>${list.acnt_dt_sbjct_name}</td>
										<td>${list.client}</td>
										<td>${list.outamt}</td>
										<td>${list.inamt}</td>
									</tr>
								</c:forEach>
							</c:if>
							
							<input type="hidden" id="totalcnt" name="totalcnt" value ="${totalcnt}"/>