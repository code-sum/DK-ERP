package kr.happyjob.study.emp.service;

import kr.happyjob.study.emp.dao.EmpDao;
import kr.happyjob.study.emp.model.EmpModel;
import kr.happyjob.study.mngNot.model.NoticeModel;
import lombok.RequiredArgsConstructor;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.Map;
@Service

public class EmpServiceImp implements EmpService{

    @Autowired
    EmpDao empDao;


    @Value("${sal_kuk_rate}")
    private String sal_kuk_rate;
    @Value("${sal_kun_rate}")
    private String sal_kun_rate;
    @Value("${sal_ko_rate}")
    private String sal_ko_rate;
    @Value("${sal_san_rate}")
    private String sal_san_rate;

    @Override
    public List<EmpModel> empList(Map<String, Object> paramMap) throws Exception {
        return empDao.empList(paramMap);
    }

    @Override
    public int countempList(Map<String, Object> paramMap) throws Exception {
        return empDao.countempList(paramMap);
    }

    @Override
    public EmpModel empSelectOne(Map<String, Object> paramMap) throws Exception {
        return empDao.empSelectOne(paramMap);
    }

    @Override
    public int empInsert(Map<String, Object> paramMap) throws Exception {
        double emp_yr_sal = (double) paramMap.get("emp_yr_sal");
        double sal_pre =emp_yr_sal/12;

        double sal_kuk = sal_pre * Integer.parseInt(sal_kuk_rate);
        double sal_kun = sal_pre * Integer.parseInt(sal_kun_rate);
        double sal_ko = sal_pre * Integer.parseInt(sal_ko_rate);
        double sal_san = sal_pre * Integer.parseInt(sal_san_rate);
        double sal_after = sal_pre - sal_kuk - sal_kun - sal_ko - sal_san;

        paramMap.put("sal_pre", sal_pre);
        paramMap.put("sal_kuk", sal_kuk);
        paramMap.put("sal_kun", sal_kun);
        paramMap.put("sal_ko", sal_ko);
        paramMap.put("sal_san", sal_san);
        paramMap.put("sal_after", sal_after);


        return empDao.empInsert(paramMap);
    }

    @Override
    public int empUpdate(Map<String, Object> paramMap) throws Exception {
        return empDao.empUpdate(paramMap);
    }

    @Override
    public int empDelete(Map<String, Object> paramMap) throws Exception {
        return empDao.empDelete(paramMap);
    }

}
