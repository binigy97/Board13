# 발견 문제점
## 1. 프로그램 실행 시 오류 직면
> **오류메세지**
```
org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'boardController': ... Cause: java.lang.ClassNotFoundException: Cannot find class: com.lec.spring.WriteDTO
```
> **원인1** : DAO.xml 에서 view.do 의 resultType 오타
```java
// 기존
resultType="com.lec.spring.WriteDTO"
// 수정
resultType="com.lec.spring.domain.WriteDTO"
```
> **원인2** : DAO.xml 에서 deleteOk.do 의 HWERE절 오타
```xml
<!-- 기존 -->
DELETE FROM test_write WHERE uid = #{uid}
<!-- 수정 -->
DELETE FROM test_write WHERE wr_uid = #{uid}
```
___
> **오류메세지**
```
Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured.

Reason: Failed to determine a suitable driver class
```
> **해결X** : application properties 에서 spring-jdbc 설정을 바꾸어 봐도 해결 못 함
___
## 2. '수정 완료'된 게시물의 uid 오류
> **원인** : updateOk.do 에서 uid 는 파라미터에 담겨서 감
```javascript
// 기존
location.href = "view.do?uid=${uid}";
// 수정
location.href = "view.do?uid=${param.uid}";
```