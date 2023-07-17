package kr.happyjob.study.accAcs.controller;

import java.io.File;
import java.net.URLEncoder;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

import javax.annotation.PostConstruct;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;

import org.apache.commons.io.FileUtils;
import org.apache.log4j.LogManager;
import org.apache.log4j.Logger;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.ResponseBody;

import kr.happyjob.study.accAcs.model.accAcsModel;
import kr.happyjob.study.accAcs.service.accAcsService;
import kr.happyjob.study.common.comnUtils.ComnCodUtil;
import kr.happyjob.study.mngNot.model.NoticeModel;
import kr.happyjob.study.mngNot.service.MngNotService;
import kr.happyjob.study.system.model.comcombo;

@Controller
@RequestMapping("/accAcs/")
public class accAcsController {
   
   @Autowired
   accAcsService AccAcsService;
   
   // Set logger
   private final Logger logger = LogManager.getLogger(this.getClass());

   // Get class name for logger
   private final String className = this.getClass().toString();
   
   
   
   /**
    * 초기화면
    */
   @RequestMapping("accountSearch.do")
   public String accountSearch(Model model, @RequestParam Map<String, Object> paramMap, HttpServletRequest request,
         HttpServletResponse response, HttpSession session) throws Exception {
      
      logger.info("+ Start " + className + ".accAcs");
      logger.info("   - paramMap : " + paramMap);
      
      logger.info("+ End " + className + ".accAcs");

      return "accAcs/accountSearchList";
      
   }
       

   /**
    * 검색
    */
   @RequestMapping("accountSearchList.do")
   public String accountSearchList(Model model, @RequestParam Map<String, Object> paramMap, HttpServletRequest request,
		   HttpServletResponse response, HttpSession session) throws Exception {
	   
	   logger.info("+ Start " + className + ".accAcs");
	   logger.info("   - paramMap12312322 : " + paramMap);
	   
	   
	   System.out.println("랄랄랄라" + paramMap);
	    
	   logger.info("+ End " + className + ".accAcs");
	   
       int pagenum = Integer.parseInt((String) paramMap.get("pagenum"));
       int pageSize = Integer.parseInt((String) paramMap.get("pageSize"));
       int pageindex = (pagenum - 1) * pageSize;
       
       paramMap.put("pageSize", pageSize);
       paramMap.put("pageindex", pageindex);
       
//       int clicombo = Integer.parseInt((String) paramMap.get("clicombo"));
//       paramMap.put("clicombo",clicombo);
//       paramMap.put("clicombo",clicombo);
//       paramMap.put("clicombo",clicombo);
       
       
       List<accAcsModel> accountSearchList = AccAcsService.accountSearchList(paramMap);
       
       int totalcnt = AccAcsService.countactlist(paramMap);
       //countnoticelist의 리턴값을 totalcnt에 대입

       
       model.addAttribute("accountSearchList", accountSearchList);
       model.addAttribute("totalcnt", totalcnt);
       //모델에 noticesearchlist, totalcnt을 등록해서 JSP로 넘기기
       
       
       
       logger.info("+ - paramMap2222222222222 " + accountSearchList);
       
       logger.info("+ End " + className + ".accountSearchList");

       return "accAcs/accountSearchListGrd";
       //"mngNot/noticelistgrd" JSP 열기
       
	   
   }
   
   
   
   @RequestMapping("accountSearchSelectone.do")
   @ResponseBody
   public Map<String, Object> accountSearchSelectone(Model model, @RequestParam Map<String, Object> paramMap, HttpServletRequest request,
         HttpServletResponse response, HttpSession session) throws Exception {
      
      logger.info("+ Start " + className + ".accountSearcheselectone");
      logger.info("   - paramMap : " + paramMap);
      
      // Controller  Service  Dao  SQL
      accAcsModel accountSearchSelectone= AccAcsService.accountSearchSelectone(paramMap);
      //mngNotService.noticeselectone(paramMap)에서 받아온 값을 모델 객체에 담기
      //이상태 그대로 그냥 JSP에 던져줘도 되지 않을까.. 왜 맵을 하나 더 키울까..
      //모델로 던지면 JSON형태로 Ajax 응답 데이터를 못받나?
      
      Map<String, Object> returnmap = new HashMap<String, Object>();
      //맵을 해시맵 형식으로 returnmap 생성 -> 맵은 인스턴스 생성이 안되기 때문에 해시맵과 같은 형태로 객체화해서 사용해야함

      returnmap.put("accountSearchSelectone", accountSearchSelectone);
      //맵에 noticesearch 키와 그에 따른 값 noticesearch을 넣어줌 
      
      logger.info("+ End " + className + ".accountSearchSelectone");

      return returnmap;
      //맵을 리턴해서 JSP에 맵을 던져줌
   }  
   
	   
	   
      
}