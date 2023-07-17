package kr.happyjob.study.emp.service;

import kr.happyjob.study.emp.dao.EmpDao;
import kr.happyjob.study.emp.model.EmpModel;
import lombok.RequiredArgsConstructor;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;
import java.util.Map;
@Service

public class EmpServiceImp implements EmpService{

    @Autowired
    EmpDao empDao;
    @Override
    public List<EmpModel> empList(Map<String, Object> paramMap) throws Exception {
        return empDao.empList(paramMap);
    }

    @Override
    public int countempList(Map<String, Object> paramMap) throws Exception {
        return empDao.countempList(paramMap);
    }
}
