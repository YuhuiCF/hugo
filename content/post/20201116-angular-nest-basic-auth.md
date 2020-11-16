---
title: 'Angular Nest Basic Auth'
date: 2020-11-16T21:15:00+02:00
lastmod: 2020-11-16T21:15:00+02:00
draft: false
tags: ['angular', 'nest']
categories: ['js']
---


## Summary

This is part of my learning in my own [my-angular-project](https://github.com/yuhuiX/my-angular-project) project.
How to use basic auth in Angular-Nest.

```javascript
// Angular
const headers: HttpHeaders = new HttpHeaders()
  .append('Authorization', 'Basic ' + btoa('name:password'));
```

```javascript
// Nest
const b64authToken: string =
  (request.headers['authorization'] || '').split(' ')[1] || '';
const [username, password] = Buffer.from(b64authToken, 'base64')
  .toString()
  .split(':');
```

<!--more-->

## Nest

The complete Nest part requires more than that code sample.

Define your injectable`LocalAuthGuard` which implements `CanActivate`:
```javascript
@Injectable()
export class LocalAuthGuard implements CanActivate {
  constructor(private authService: AuthService) {}

  canActivate(context: ExecutionContext): boolean | Promise<boolean> {
    const request = context.switchToHttp().getRequest() as Request;

    const b64authToken: string =
      (request.headers['authorization'] || '').split(' ')[1] || '';
    const [username, password] = Buffer.from(b64authToken, 'base64')
      .toString()
      .split(':');

    return this.authService.areUserCredentialsValid({ username, password });
  }
}
```

```javascript
controller {
  // Nest way of doing authentication using Guards
  // can be moved to the controller and will then be applied to the whole controller
  @UseGuards(LocalAuthGuard)
  @Post()
  createXXX() {}
}
```
