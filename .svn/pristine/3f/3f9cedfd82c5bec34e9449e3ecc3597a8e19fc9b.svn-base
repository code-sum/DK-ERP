package kr.happyjob.study.empApm.service;

import java.io.File;
import java.util.List;
import java.util.Map;

import javax.servlet.http.HttpServletRequest;

import org.apache.log4j.LogManager;
import org.apache.log4j.Logger;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Service;
import org.springframework.web.multipart.MultipartHttpServletRequest;

import kr.happyjob.study.empApm.dao.EmpApmDao;
import kr.happyjob.study.empApm.model.EmpApmModel;
import kr.happyjob.study.common.comnUtils.FileUtilCho;



@Service
public class EmpApmServiceImpl implements EmpApmService {

	// Set logger
	private final Logger logger = LogManager.getLogger(this.getClass());
	
	// Get class name for logger
	private final String className = this.getClass().toString();
	
	@Autowired
	EmpApmDao empApmDao;
	
	@Value("${fileUpload.rootPath}")
	private String rootPath;    // W:\\FileRepository
	
	@Value("${fileUpload.virtualRootPath}")
	private String virtualrootPath;  // /serverfile
	
	@Value("${fileUpload.noticePath}")
	private String noticePath;   // notice
		
	
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
	
	
	/** 수정 */
	public int listUpdateApm(Map<String, Object> paramMap) throws Exception {
		paramMap.put("fileprc", "N");
		empApmDao.listUpdateApm(paramMap);
		return empApmDao.listUpdateApproApm(paramMap);
	}
	
	
	
	/** 수정 파일 */
	public int listUpdateFileApm(Map<String, Object> paramMap, HttpServletRequest request) throws Exception {
		empApmDao.listUpdateFileApproApm(paramMap);	
		return empApmDao.listUpdateFileBudApm(paramMap);
			
		
	}
	

	
	
}
