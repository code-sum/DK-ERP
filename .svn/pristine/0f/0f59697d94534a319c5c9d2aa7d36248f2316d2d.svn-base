package kr.happyjob.study.accEps.service;

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

import kr.happyjob.study.accEps.dao.AccEpsDao;
import kr.happyjob.study.accEps.model.AccEpsModel;
import kr.happyjob.study.common.comnUtils.FileUtilCho;



@Service
public class AccEpsServiceImpl implements AccEpsService {

	// Set logger
	private final Logger logger = LogManager.getLogger(this.getClass());
	
	// Get class name for logger
	private final String className = this.getClass().toString();
	
	@Autowired
	AccEpsDao accEpsDao;
	
	@Value("${fileUpload.rootPath}")
	private String rootPath;    // W:\\FileRepository
	
	@Value("${fileUpload.virtualRootPath}")
	private String virtualrootPath;  // /serverfile
	
	@Value("${fileUpload.noticePath}")
	private String noticePath;   // notice
		
	
	/** 목록 조회 */
	public List<AccEpsModel> expenseSearchList(Map<String, Object> paramMap) throws Exception {
		
		return accEpsDao.expenseSearchList(paramMap);
	}
	
	/** 목록 카운트 조회 */
	public int countList(Map<String, Object> paramMap) throws Exception {
				
		return accEpsDao.countList(paramMap);
	}
	
	/** 한건 조회 */
	public AccEpsModel listSelectOneEps(Map<String, Object> paramMap) throws Exception {
		
		return accEpsDao.listSelectOneEps(paramMap);
	}
	
	/** 등록 */
	public int listInsertEps(Map<String, Object> paramMap) throws Exception {		
		accEpsDao.listInsertEps(paramMap);
		return accEpsDao.approInsertEps(paramMap); 
	}
	
	/** 수정 */
	public int listUpdateEps(Map<String, Object> paramMap) throws Exception {
		paramMap.put("fileprc", "N");
		accEpsDao.listUpdateEps(paramMap);
		return accEpsDao.listUpdateApproEps(paramMap);
	}
	
	/** 삭제 */
	public int listDeleteEps(Map<String, Object> paramMap) throws Exception {
		return accEpsDao.listDeleteEps(paramMap);
	}
	
	/** 등록 파일 */
	public int listInsertFileEps(Map<String, Object> paramMap, HttpServletRequest request) throws Exception {
		
		MultipartHttpServletRequest multipartHttpServletRequest = (MultipartHttpServletRequest) request;
		
		// private String rootPath;    // W:\\FileRepository
		// private String virtualrootPath;  // /serverfile
		// private String noticePath;   // notice
		
		String noticedir = File.separator + noticePath + File.separator;
		FileUtilCho fileup = new FileUtilCho(multipartHttpServletRequest,rootPath, virtualrootPath, noticedir);
		Map filereturn = fileup.uploadFiles();
		
		//map.put("file_nm", file_nm);
        //map.put("file_size", file_Size);
        //map.put("file_loc", file_loc);
        //map.put("vrfile_loc", vrfile_loc);
        //map.put("fileExtension", fileExtension);
		
		String upfile = (String) filereturn.get("file_nm");
		paramMap.put("fileprc", "Y");
		
		if(upfile == "" || upfile == null) {
			paramMap.put("fileexist", "N");
		} else {
			paramMap.put("filereturn", filereturn);
			paramMap.put("fileexist", "Y");
			
			accEpsDao.fileinsertEps(paramMap);
		}
		
		accEpsDao.approInsertEps(paramMap); 
		
		return accEpsDao.listInsertEps(paramMap);
	}
	
	/** 수정 파일 */
	public int listUpdateFileEps(Map<String, Object> paramMap, HttpServletRequest request) throws Exception {
		
		return accEpsDao.listUpdateFileApproEps(paramMap);		
		
	}
	
	/** 삭제  파일*/
	public int listDeleteFileEps(Map<String, Object> paramMap) throws Exception {
		
        AccEpsModel selectone = accEpsDao.listSelectOneEps(paramMap);
		
		if(selectone.getFile_name() != "" && selectone.getFile_name() != null) {
			File attfile = new File(selectone.getPhysic_path());     
			attfile.delete();
			
			//notice_no			
			// tb_file delete
			accEpsDao.deletefileinfoEps(paramMap);
		} 
		accEpsDao.listDeleteEps(paramMap);
		return accEpsDao.listDeleteApproEps(paramMap);
	}
	
	
	
}
