# Axios

Axios는 브라우저와 node.js를 위한 간단한 Promise 기반 HTTP 클라이언트이다. Axios는 매우 확장 가능한 인터페이스를 가진 패키지로 사용하기 쉬운 라이브러리를 제공한다.

1. Axios 설치
    
    ```jsx
    npm install axios
    ```
    

1. Axios 기본 사용법
    
    ```jsx
    axios({
    	method: "get",
    	url: "url",
    	responseType: "type"
    }).then(function (response) {
    	// response action
    }).catch(function (error) {
    	// error action
    })
    ```
    
    *Axios 응답 제어*
    
    만약 POST 메서드에서 data를 전송하기 위해서는 url 밑에 Object를 추가하면 된다.
    
    - **then**: 비동기 통신이 성공했을 경우 .then()은 콜백을 인자로 받아 결과값을 처리할 수 있다.
    - **catch**: catch()를 통해 오류를 처리한다. error 객체에서는 오류에 대한 주요 정보를 확인할 수 있다.

1. Axios HTTP 요청 메서드 종류
- **axios.get(url[, config])**: 서버에서 데이터를 가져올 때 사용하는 메서드. 두 번째 파라미터 config 객체에는 헤더(header), 응답 초과시간(timeout), 인자값(params) 등의 요청값을 같이 넘길 수 있다.
- **axios.post(url[, data[, config]])**: 서버에 데이터를 새로 생성할 때 사용하는 메서드. 두 번째 파라미터 data에 생성할 데이터를 넘긴다.
- **axios.put(url[, data[, config]])**: 특정 데이터를 수정할 때 요청하는 메서드. put은 새로운 리소스를 생성하거나, 이미 존재하는 데이터를 대체할 때 사용된다. post와 다른 점은 post는 여러번 호출할 경우, 새로운 데이터가 지속적으로 추가되는 반면, pust은 한 번 요청하거나 여러번 지속적으로 요청해도 결과값이 동일하다.
- **axios.delete(url[, config])**: 특정 데이터나 값을 삭제할 때 사용하는 메서드.

1. Axios HTTP 요청 Config 옵션
- **method**: 요청할 때 사용할 요청 메서드. method의 기본값은 GET이다.
- **url**: axios 요청에 사용될 URL이다.
- **baseURL**: axios 인스턴스를 생성할 때, 인스턴스의 기본 URL값을 정할 수 있는 속성. 보통 API 서버의 기본 도메인을 설정하고, 인스턴스별로 URL을 뒤에 추가하여 사용한다.
- **headers**: header를 수정해서 보내야한다면 headers를 사용한다.
- **params**: HTTP 요청에 붙일 URL 파라미터를 의미한다. params가 null이나 undefined인 경우 파라미터가 조합되지 않는다.
- **data**: HTTP 요청 Body에 실어서 보낼 데이터를 의미한다. 주로 데이터를 조작해야 하는 PUT, POST, DELETE, PATCH 등의 메서드에서 사용한다.
- **timeout**: HTTP 요청을 보내고 응답을 받기까지의 제한 시간을 설정하는 속성이다. 요청 시간이 지정된 값을 초과하면 에러가 발생한다.
- **responseType**: 서버로부터 어떠한 데이터 형식으로 응답받을지를 지정하는 것이다. 옵션으로는 arraybuffer, document, json, text, stream이 가능하다. 기본값은 json이다.

1. 단축된 Axios 메서드
    1. axios.get()
        - 단순 데이터(페이지 요청, 지정된 요청)을 수행할 경우
        - 파라미터 데이터를 포함시키는 경우(사용자 번호에 따른 조회)
        
        2가지 상황에 따라 params: {} 객체가 존재할지 안할지 결정된다.
        
        - **단순 데이터를 요청할 경우**
            
            ```jsx
            // callback을 사용할 때,
            axios.get("URL")
            	.then(function (response) {
            		// response
            	})
            	.catch(function (error) {
            		// error 발생시 실행
            	})
            	.then(function () {
            		// 항상 실행
            	});
            
            // async await 함수를 사용할 때,
            try {
            	const data = await axios.get("URL");
            } catch {
            	// 오류 발생시 실행
            }
            ```
            
        - **파라미터 데이터를 포함시키는 경우**
            
            ```jsx
            axios.get("URL", {
            	params: {
            		id: 123
            	}
            })
            .then(function (response) {
            	// response
            })
            .catch(function (error) {
            	// 오류 발생시 실행
            })
            .then(function () {
            	// 항상 실행
            });
            
            // async await 함수를 사용할 때,
            try {
            	const data = await axios.get("URL", params: { id: 123 });
            } catch {
            	// 오류 발생시 실행
            }
            ```
            
    2. axios.post()
        
        post 메서드에는 일반적으로 데이터를 Message Body에 포함시켜 보낸다.
        
        ```jsx
        axios.post("URL", {
        	username: "",
        	password: ""
        })
        .then(function (response) {
        })
        .catch(function (error) {
        })
        .then(function () {
        });
        
        try {
        	const data = await axios.poset("URL");
        } catch {
        }
        ```
        
    3. axios.put()
        
        put 메서드는 서버 내부적으로 get → post 과정을 거치기 때문에 post 메서드와 비슷한 형태이다.
        
        ```jsx
        axios.put("URL", {
        	username: "",
        	password: ""
        })
        .then(function (response) {
        })
        .catch(function (error) {
        })
        .then(function (response) {
        });
        
        try {
        	const data = await axios.put("URL", { username: "", password: "" });
        } catch {
        }
        ```
        
    4. axios.delete()
        
        delete 메서드에는 일반적으로 body가 비어있다. 그래서 get과 비슷한 형태를 띄지만 한 번 delete 메서드가 서버에 들어가게 된다면 서버 내에서 삭제 process를 진행하게 된다.
        
        - **일반적인 delete**
            
            ```jsx
            axios.delete("/user?id=12345")
            .then(function (response) {
            	// handle success	
            	console.log(response);
            })
            .catch(function (error) {
            	// handle error
            	console.log(error);
            })
            .then(function () {
            	// always executed
            });
            
            try {
            	const data = await axios.delete("URL");
            } catch {
            }
            ```
            
        - **많은 데이터를 요청할 경우**
            
            query나 params가 많아져 헤더에 정보를 담을 수 없을 때는 두번째 인자에 data를 추가해줄 수 있다.
            
            ```jsx
            axios.delete("/user?id=12345", {
            	data: {
            		post_id: 1,
            		comment_id: 13,
            		username: "foo"
            	}
            })
            .then(function (response) {
            })
            .catch(function (error) {
            })
            .then(function () {
            });
            ```
            
        
        ---
        
        ### View 프로젝트에서 axios 사용
        
        utils 폴더에 request 항목을 만들고, api를 호출하기 위한 base.api.request를 만들어준다.
        
        Request 요청에 대한 timout 설정을 해준다. Default로 3분으로 설정했다.
        
        ```jsx
        import axios from 'axios'
        import Store from '@/store/index'
        
        const REQUEST_TIMEOUT = 180000;
        ```
        
        Class를 만들어 외부 자바스크립트에서 호출한 뒤 쉽게 사용할 수 있도록 했다.
        
        ```jsx
        const BaseApiRequest = class BaseApiRequest {
        	/** axios 인스턴스를 초기화한 다음 요청 및 응답 인터셉터를 설정
        		* @param base_url - API의 기본 URL.
        		**/
        	
        	constructor(base_url) {
        		this.init_axios(base_url);
        		this.init_axios_request_interceptor();
        		this.init_axios_response_interceptor();
        	}
        
        	init_axios(base_url) {
        		this.axios = axios.create({
        			baseURL: base_url,
        			timeout: REQUEST_TIMEOUT
        		});
        	}
        
        	init_axios_request_interceptor() {
        		this.axios.interceptors.request.use(
        			(config) => {
        				setAxiosRequestConfig(config);
        				return config;
        			},
        			(error) => {
        				writeLogIfDevelopment(E_LOG_LEVEL.error, error);
        				return Promise.resolve(error);
        			}
        		);
        	}
        
        	init_axios_response_interceptor() {
        		this.axios.interceptors.response.use(
        			(response) => {
        				/** Response가 성공일 때 로직
        					*/
        				writeLogIfDevelopment(E_LOG_LEVEL.info, response);
        				return response;
        			},
        			async (error) => {
        				/** 글로벌 에러 처리가 필요한 경우 이곳에 작성
        					*/
        				const response = error.response;
        				const originalConfig = error.config;
        				writeLogIfDevelopment(E_LOG_LEVEL.error, response);
        	
        				if (response.status === 401 && !originalConfig._retry) {
        					originalConfig._retry = true;
        					try {
        						const form = new FormData();
        						form.append("token", Store.getters["user/getRefreshToken"]);
        						
        						const rs = await this.axios.post("/auth/refresh", form);
        						const accessToken = rs.headers["authorization"];
        
        						Store.commit("user/SET_ACCESS_TOKEN", accessToken);
        
        						return this.axios.request(originalConfig);
        					} catch (_error) {
        						await Store.dispatch("user/logout");
        						return Promise.resolve(_error);
        					}
        				}
        
        				await handleStatusCode(response.status);
        
        				return Promise.resolve(response);
        			}
        		);
        	}
        
        	get(url, params) {
        		return this.axios.get(url, {
        			params: params
        		});
        	}
        
        	post(url, data, config) {
        		return this.axios.post(url, data, config);
        	}
        
        	put(url, data) {
        		return this.axios.put(url, data);
        	}
        
        	delete(url, params) {
        		return this.axios.delete(url, {
        			params: params
        		});
        	}
        
        	patch(url, data) {
        		return this.axios.patch(url, data);
        	}
        }
        ```
        
        ```jsx
        export const internalAPIRequest = new BaseApiRequest(process.env.VUE_APP_BASE_API_DOMAIN + process.env.VUE_APP_INTERNAL_API_URI);
        ```
        
        api 호출시 base.api.request import 한 뒤 간편하게 사용할 수 있다.
        
        ```jsx
        import { internalAPIRequest } from '@/util/request/base.api.request';
        
        export function functionName(params) {
        	return internalAPIRequest.get(`URL`);
        }
        ```
        
        - internalAPIRequest.get()
        - internalAPIRequest.post()
        - internalAPIRequest.put()
        - internalAPIRequest.delete()
        - internalAPIRequest.patch()
        
        등 설계된 API에 맞춰 파라미터 및 옵션을 추가해서 보내주면 된다.
