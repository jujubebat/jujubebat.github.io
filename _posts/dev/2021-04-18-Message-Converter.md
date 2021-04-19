---
title: "Spring 메세지 컨버터"
categories:
  - dev
tags:
  - Java
  - Spring
---

@RequestBody와 @ResponseBody를 사용하면, HTTP 요청 본문과 HTTP 응답 본문을 통째로 다룰 수 있다. 이때 HTTP 요청, 응답간에 데이터 변환을 담당하는 것이 `메세지 컨버터`다.

#### 메세지 컨버터 종류

![R1280x0-3](https://user-images.githubusercontent.com/37281119/115141088-80f3a100-a075-11eb-8a7b-3019f26b26d1.png)

Json 데이터를 변환해주는 Jackson 메세지 컨버터를 사용한다고 가정하고 아래 코드를 살펴보자

#### @RquestBody

```java
@PostMapping(value = "/pieces")
public void postPieces(@RequestBody PiecesRequestDto piecesRequestDto) {
	return chessService.postPieces(piecesRequestDto);
}
```

위 컨트롤러 메서드의 인자에 @RequestBody 어노테이션과 함께 객체가 선언 되어있다. 예를들어 클라이언트가 `PiecesRequestDto` 와 같은 json 데이터를 HTTP 본문에 담아 POST 요청을 보낸다면 메세지 컨버터는 json을 PiecesRequestDto 객체로 변환하여 메서드의 인자로 넣어준다. 

#### @ResponseBody

```java
@GetMapping(value = "/rooms")
public RoomsResponseDto getRooms() {
    return chessService.getRooms();
}
```

위 컨트롤러 메서드에서는 RoomsResponseDto 객체를 반환하고 있다. 메서지 컨버터는 RoomsResponseDto 객체를 json 형태로 변환해주고, HTTP 본문에 담아 응답한다. 



