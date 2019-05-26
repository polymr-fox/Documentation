
# Запросы


## Авторизация:

    • порт – 9991
    
    • /auth - { username:””, password:””}
    
    • /reg – {username:””, password:””, fullName:””, role:””, mail:””}
    
    • /update_jwt – передайте старый жвт в хэдэре типом Bearer authorization
    
    • /update_pass - {username:””, password:””, additionalInfo:”new pass”}
    
    • /forgot_pass - {username:””, password:””, additionalInfo:”mail”}
    

## Статьи:

    • порт – 9992
    
    • /create – {articleName:””, text:””, tags:[“”, “”, “”], creatorId:””}
    
    • /delete – {id:_}
    
    • /read
    
    • /read/usr – {fullName:””}
    
    • /read/usr/rtg – {fullName:””}
    
    • /read/rtg – {rating:_}
    
    • /update/rtg – {id:_, rating:_}
    
    • /update – {id:_, articleName:””, text:””, tags:[“”, “”, “”]}
    

## Курсы:

    • порт – 9993
    
    • /create – 
    
        ◦ {creatorId:_, courseName:””, courseDescription:””, adminIds:[_, _, _], userIds:[_, _, _], tags:[“”, “”, “”], isOpen:true} 
        
    • /read
    
    • /read/usr – {fullName:””}
    
    • /read/rtg – {rating:_}
    
    • /subscribe – {id:_, userId:_}
    
    • /unsubscribe - {id:_, userId:_}
    
    • /change - {id:_, userId:_, isOpen:_}
    
    • /update - 
    
        ◦ {id:_, name:””, description:””,  adminIds:[_, _, _], userIds:[_, _, _], tags:[“”, “”, “”], isOpen:true}
        
    • /delete – {id:_}
    

# Ответы


## Авторизация:

    • порт – 9991
    
    • /auth - 
        
        ◦ ok - 200 OK {userId:__, userName:"", fullName:"", mail:"", links:[{},{}], role:"", canTags:[{},{}], loveTags:[{},{}], token:""}
        ◦ okn't - 
            ◦ недопустимые символы - 400 bad request {status: 400, error:”Illegal character”, message:"Illegal characters inlogin/password", path:”/auth”}
            ◦ не прошел авторизацию - 401 Unauthorized {status: 401, error:"Unauthorized", message: "Wrong login or password", path:"/auth"}
    
    • /reg – 
        
        ◦ ok - 200 OK {userId:__, userName:"", fullName:"", mail:"", links:[{},{}], role:"", canTags:[{},{}], loveTags:[{},{}], token:""}
        ◦ okn't - 409 conflict {status = 409, error = "Conflict", message = "User with such username or mail already exist. Choose another one.", path = "/reg"}
    
    • /update_jwt – 
        ◦ ok - 200 OK {token:""}
        ◦ okn't - 
            ◦ неверный jwt - 401 Unauthorized {status = 401, error = "Unauthorized", message = "Wrong Jwt, auth again by /auth", path = "/update_jwt" }
            ◦ в хэдэре нет токена - 401 Unauthorized {status = 401, error = "Unauthorized", message = "No token in header provided", path = "/update_jwt"}
    
    • /update_pass - //doesn't work
    
    • /forgot_pass - //doesn't work
    

## Статьи:

    • порт – 9992
    
    • /create – 
    
        ◦ ok - {id:_, creatorId:_, articleName:””, articleText:””, tags:[“”, “”], date:””} // (1)
        
        ◦ okn’t – 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/create”}
        
    • /delete – 
    
        ◦ ok – 200 OK
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/delete”}
        
    • /read - 
    
        ◦ ok – {articles: [{}, {}, {}]} //массив (1)
        
        ◦ okn’t – 400 bad request {status: 400, error:”Bad request”, message:”DataBase is empty.”, path:”/read”}
        
    • /read/user – 
    
        ◦ ok - {articles: [{}, {}, {}]} //массив (1)
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/read/user”}
        
    • /read/user/rating – 
    
        ◦ ok - {articles: [{}, {}, {}]} //массив (1)
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/read/user/rating”}
        
    • /read/rating – 
    
        ◦ ok - {articles: [{}, {}, {}]} //массив (1)
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/read/rating”}
        
    • /update/rating – 
    
        ◦ ok - {id:_, creatorId:_, articleName:””, articleText:””, tags:[“”, “”], date:””} // (1)
        
        ◦ okn’t – 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/update/rating”}
        
    • /update – 
    
        ◦ ok - {id:_, creatorId:_, articleName:””, articleText:””, tags:[“”, “”], date:””} // (1)
        
        ◦ okn’t – 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/update/rating”}
        

## Курсы:

    • порт – 9993
    
    • /create – 
    
        ◦ ok - {id: _, creatorId:_, courseName:””, courseDescription:””, adminIds:[_, _, _], userIds:[_, _, _], tags:[“”, “”, “”], isOpen:true, date:””}
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/create”}
        
    • /read
    
        ◦ ok – {courses:[{}, {}, {}]}//массив курсов
        
        ◦ okn’t – 400 bad request {status: 400, error:”Bad request”, message:”DataBase is empty.”, path:”/read”}
        
    • /read/user – 
    
        ◦ ok – {courses:[{}, {}, {}]}//массив курсов
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/read/user”}
        
    • /read/rtg – 
    
        ◦ ok – {courses:[{}, {}, {}]}//массив курсов
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/read/rating”}
        
    • /subscribe – 
    
        ◦ ok - {id: _, creatorId:_, courseName:””, courseDescription:””, adminIds:[_, _, _], userIds:[_, _, _], tags:[“”, “”, “”], isOpen:true, date:””}
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/subscribe”}
        
    • /unsubscribe - 
    
        ◦ ok - {id: _, creatorId:_, courseName:””, courseDescription:””, adminIds:[_, _, _], userIds:[_, _, _], tags:[“”, “”, “”], isOpen:true, date:””}
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/unsubscribe”}
        
    • /update - 
    
        ◦ ok - {id: _, creatorId:_, courseName:””, courseDescription:””, adminIds:[_, _, _], userIds:[_, _, _], tags:[“”, “”, “”], isOpen:true, date:””}
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/update”}
        
    • /delete – 
    
        ◦ ok – 200 OK
        
        ◦ okn’t - 400 bad request {status: 400, error:”Bad request”, message:”Bad request with: {пришедший запросом жсон}, path:”/delete”}
        
