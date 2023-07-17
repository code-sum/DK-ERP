package kr.happyjob.study.accAcm.controller;

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

import kr.happyjob.study.accAcm.model.accAcmModel;
import kr.happyjob.study.accAcm.service.accAcmService;
import kr.happyjob.study.accAcs.model.accAcsModel;
import kr.happyjob.study.common.comnUtils.ComnCodUtil;
import kr.happyjob.study.mngNot.model.NoticeModel;
import kr.happyjob.study.mngNot.service.MngNotService;

@Controller
@RequestMapping("/accAcm/")
public class accAcmController {
   
   @Autowired
   accAcmService AccAcmService;
   
   // Set logger
   private final Logger logger = LogManager.getLogger(this.getClass());

   // Get class name for logger
   private final String className = this.getClass().toString();
   
   
   
   /**
    * 초기화면
    */
   @RequestMapping("accManagement.do")
   public String notice(Model model, @RequestParam Map<String, Object> paramMap, HttpServletRequest request,
         HttpServletResponse response, HttpSession session) throws Exception {
      
      logger.info("+ Start " + className + ".accAcm");
      logger.info("   - paramMap : " + paramMap);
      
      logger.info("+ End " + className + ".accAcm");

      return "accAcm/accAcmList";
   }

   /**
    * 검색
    */
   @RequestMapping("accManagementList.do")
   public String accManagementList(Model model, @RequestParam Map<String, Object> paramMap, HttpServletRequest request,
		   HttpServletResponse response, HttpSession session) throws Exception {
	   
	   logger.info("+ Start " + className + ".accAcm");
	   logger.info("   - paramMap12312322 : " + paramMap);
	   
	   
	   System.out.println("랄랄랄라" + paramMap);
	    
	   logger.info("+ End " + className + ".accAcm");
	   
       int pagenum = Integer.parseInt((String) paramMap.get("pagenum"));
       int pageSize = Integer.parseInt((String) paramMap.get("pageSize"));
       int pageindex = (pagenum - 1) * pageSize;
       
       paramMap.put("pageSize", pageSize);
       paramMap.put("pageindex", pageindex);
       
       
       
       List<accAcmModel> accAcmSearchList = AccAcmService.accAcmSearchList(paramMap);
       
       int totalcnt = AccAcmService.countactlist(paramMap);
       //countnoticelist의 리턴값을 totalcnt에 대입

       
       model.addAttribute("accAcmSearchList", accAcmSearchList);
       model.addAttribute("totalcnt", totalcnt);
       //모델에 noticesearchlist, totalcnt을 등록해서 JSP로 넘기기
       
       
       
       logger.info("+ - paramMap2222222222222 " + accAcmSearchList);
       
       logger.info("+ End " + className + ".accountSearchList");

       return "accAcm/accAcmListGrd";
       
	   
   }
   
   
   
   
   
	   
      
}