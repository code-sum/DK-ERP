package kr.happyjob.study.emp.controller;

import kr.happyjob.study.emp.model.EmpModel;
import kr.happyjob.study.emp.service.EmpService;
import org.apache.log4j.LogManager;
import org.apache.log4j.Logger;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import java.util.List;
import java.util.Map;

@Controller
@RequestMapping("/empEpm/")
public class empController {

     @Autowired
     EmpService empService;

    private final Logger logger = LogManager.getLogger(this.getClass());
    private final String className = this.getClass().toString();

    @RequestMapping("/empmanagement.do")
    public String emp(Model model, @RequestParam Map<String, Object> paramMap, HttpServletRequest request,
                      HttpServletResponse response, HttpSession session)throws Exception{
        logger.info("+ Start " + className  + ".emp");
        logger.info("   - paramMap : " + paramMap);

        logger.info("+ End " + className + ".notice");

        return "emp/empList";

    }
    @RequestMapping("emplist.do")
    public String noticelist(Model model, @RequestParam Map<String, Object> paramMap, HttpServletRequest request,
                             HttpServletResponse response, HttpSession session) throws Exception {

        logger.info("+ Start " + className + ".emplist");
        logger.info("   - paramMap : " + paramMap);

        int pagenum = Integer.parseInt((String) paramMap.get("pagenum"));
        int pageSize = Integer.parseInt((String) paramMap.get("pageSize"));
        int pageindex = (pagenum - 1) * pageSize;

        paramMap.put("pageSize", pageSize);
        paramMap.put("pageindex", pageindex);

        // Controller  Service  Dao  SQL
        List<EmpModel> empSearchList = empService.empList(paramMap);
        int totalcnt = empService.countempList(paramMap);

        model.addAttribute("empSearchList", empSearchList);
        model.addAttribute("totalcnt", totalcnt);


        logger.info("+ End " + className + ".emplist");

        return "emp/emplistgrd";
    }
}
