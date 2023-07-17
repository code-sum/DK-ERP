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
  <c:forEach items="${empSearchList}" var="list">
    <tr>
      <td>${list.loginId}</td>
      <td><a href="javascript:fn_empSelectOne('${list.loginId}')">${list.name}</a></td>
      <td>${list.dept_cd}</td>
      <td>
      <select id="deptcd" name="deptcd">
        <option value="" >전체</option>
        <option value="100" <c:if test ="${list.dept_cd eq '100'}">selected="selected"</c:if>>관리자</option>
        <option value="200" <c:if test ="${list.dept_cd eq '200'}">selected="selected"</c:if>>임원직</option>
        <option value="300" <c:if test ="${list.dept_cd eq '300'}">selected="selected"</c:if>>회계팀</option>
        <option value="400" <c:if test ="${list.dept_cd eq '400'}">selected="selected"</c:if>>영업팀</option>
        <option value="500" <c:if test ="${list.dept_cd eq '500'}">selected="selected"</c:if>>인사팀</option>
      </select>
      </td>
      <td>
        <select id="lvcd" name="lvcd">
          <option value="" >전체</option>
          <option value="10"<c:if test ="${list.level_cd eq '10'}">selected="selected"</c:if>>사원</option>
          <option value="20"<c:if test ="${list.level_cd eq '20'}">selected="selected"</c:if>>주임</option>
          <option value="30"<c:if test ="${list.level_cd eq '30'}">selected="selected"</c:if> >대리</option>
          <option value="40"<c:if test ="${list.level_cd eq '40'}">selected="selected"</c:if> >과장</option>
          <option value="50"<c:if test ="${list.level_cd eq '50'}">selected="selected"</c:if> >부장</option>
          <option value="60"<c:if test ="${list.level_cd eq '60'}">selected="selected"</c:if> >상무</option>
          <option value="70"<c:if test ="${list.level_cd eq '70'}">selected="selected"</c:if> >전무</option>
          <option value="80"<c:if test ="${list.level_cd eq '80'}">selected="selected"</c:if> >이사</option>
          <option value="90"<c:if test ="${list.level_cd eq '90'}">selected="selected"</c:if> >대표</option>
        </select>
      </td>
      <td>${list.emp_sdate}</td>
      <td>${list.emp_work_yn}</td>
    </tr>
  </c:forEach>
</c:if>

<input type="hidden" id="totalcnt" name="totalcnt" value ="${totalcnt}"/>