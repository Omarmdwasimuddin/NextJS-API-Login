## NextJS-API-Login

### User Login API with JWT Authentication
![](https://imgur.com/ueFPNli.png)

```bash
import { SignJWT } from "jose";
import { NextRequest, NextResponse } from "next/server";



export async function POST(request:NextRequest) {
    
    const json = await request.json();
    let userName = json['user'];
    let password = json['password'];

    if (userName === 'Wasim' && password === 'wasim123') {
        
        const Key = new TextEncoder().encode(process.env.JWT_KEY);
        const payload = {userName: userName}

        let token = await new SignJWT(payload)
            .setProtectedHeader({ alg: 'HS256' })
            .setIssuedAt()
            .setIssuer('https://localhost:3000')
            .setExpirationTime('2h')
            .sign(Key)

        return NextResponse.json(
            {status: "Success", message: "Login Success!", token:token},
            {status: 200}
        )
    }else {
        console.error("Invalid login attempt for user:", userName);
        return NextResponse.json(
            {status: "Fail", message: "Invalid user"},
            {status: 401}
        )
    }

}
```
---
