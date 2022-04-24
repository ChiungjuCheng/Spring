# Controller
使用類別

```java
import org.springframework.web.multipart.MultipartFile;
import org.springframework.web.bind.annotation.RequestPart;
@Slf4j
@RequestMapping("images")
@RestController
public class ImageController {

	@PostMapping("/upload")
	String imagesUpload(@RequestPart("file") MultipartFile file,
    	@RequestPart("uploadFileReqDTO") UploadFileReqDTO uploadFileReqDTO) {

		log.info(String.valueOf(file.getSize()));
		log.info(uploadFileReqDTO.toString());

		return "ok";
	}
}
```

# Postman sending request
![MultipartFile and json](/Sending%20different%20content%20types/multipart_and_json_postman.png)