package kr.happyjob.study.empApm.service;

import java.util.List;
import java.util.Map;

import javax.servlet.http.HttpServletRequest;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import kr.happyjob.study.empApm.dao.EmpApmDao;
import kr.happyjob.study.empApm.model.EmpApmModel;

@Service
public class EmpApmServiceImpl implements EmpApmService {

	// // Set logger
	// private final Logger logger = LogManager.getLogger(this.getClass());
	//
	// // Get class name for logger
	// private final String className = this.getClass().toString();

	@Autowired
	EmpApmDao empApmDao;

	/** 목록 조회 */
	public List<EmpApmModel> approManagementList(Map<String, Object> paramMap) throws Exception {
		return empApmDao.approManagementList(paramMap);
	}

	/** 목록 카운트 조회 */
	public int countList(Map<String, Object> paramMap) throws Exception {

		return empApmDao.countList(paramMap);
	}

	/** 한건 조회 */
	public EmpApmModel listSelectOneApm(Map<String, Object> paramMap) throws Exception {

		return empApmDao.listSelectOneApm(paramMap);
	}

	@Override
	public EmpApmModel getVacationStatus(Map<String, Object> paramMap) throws Exception {
		return empApmDao.getVacationStatus(paramMap);
	}
	
	
	public int updateApmStatus(Map<String, Object> paramMap) throws Exception {
		return empApmDao.updateApmStatus(paramMap);
	}
	public int listUpdateFileBudApm(Map<String, Object> paramMap) throws Exception{
		return empApmDao.listUpdateFileBudApm(paramMap);
	}
/*	@Override
	public EmpApmModel getVacationStatus(Map<String, Object> paramMap) throws Exception {
		return empApmDao.getVacationStatus(paramMap);
	}*/


}
