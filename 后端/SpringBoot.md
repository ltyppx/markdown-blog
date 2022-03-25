# 文章目录
## SpringBoot自定义配置
### SpringBoot的核心配置文件
SpringBoot核心配置文件为resources文件夹内的application.properties文件

application.properties值的格式为： ``object.item.key=value`` 

SpringBoot核心配置文件后缀除了为properties，还能为yml或yaml

application.yml和application.yaml值的格式为 ：
```
object:
    item:
        key: value
``` 

要注意SpringBoot核心配置文件后缀有三种，但是名称必须为application，且只能有一个

SpringBoot核心配置文件可以根据环境匹配相应的核心配置文件

根据环境匹配的核心配置文件必须按规定的格式命名 ``application-{自定义}.{properties|yml|yaml}``

然后在application.properties中引入 ``server.servlet.context-path=/自定义``

## SpringBoot拦截器
### 创建拦截器
```
package com.springboot.test.interceptor;

import com.springboot.test.model.User;
import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class UserInterceptor implements HandlerInterceptor {

    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        User user = (User) request.getSession().getAttribute("user");
        if(user == null) {
            response.sendRedirect(request.getContextPath() + "/user/nologin");
            return false;
        }
        return true;
    }

    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {

    }

    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {

    }

}

```
### 定义拦截配置
```
package com.springboot.test.config;

import com.springboot.test.interceptor.UserInterceptor;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
public class InterceptorConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        String[] addPathPatterns = {
            "/user/*",
        };

        String[] excludePathPatterns = {
                "/user/login",
                "/user/nologin",
        };

        registry.addInterceptor(new UserInterceptor()).addPathPatterns(addPathPatterns).excludePathPatterns(excludePathPatterns);
    }
}

```