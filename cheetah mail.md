#Cheetah Mail

```

var cookie = null;


function send_to_cheetah(req, res) {
  res.header("Access-Control-Allow-Origin", "*");
  // console.log( "Sending to Cheetah");
  // console.log( "Cookie: " + cookie );
  if (cookie === null) {
    console.log( "Not Authenticated, Renewing Cookie");
    cheetah_renew(req, res);
    return;
  } else {
    //Check if cookie has expired
    var rightNow = new Date();
    //Grab experation date from cookie
    var ca = cookie.split(';');
    var date = ca[3].split('=');
    if ( Date.parse(date[1]) <= Date.parse(rightNow) ) {
      cheetah_renew(req, res);
      return;
    } else {
      console.log ("Cookie is still good!");
    }
  }
  
  var email = req.query.email;
  var name = req.query.name;

  // console.log ("Email: " + email);
  // console.log ("Name: " + name);
  // console.log("Calling setUser1");

  request.get(
    {
        uri: 'https://ebm.cheetahmail.com/api/setuser1',
        headers: {
            'Cookie': cookie
        },
        qs: {
          "sub" : "2088064674",
          "SOURCE" : "wxyz",
          "email" : email,
          "name" : name,
          "aid" : "2087899051",
          "e" : "233783"
        }
    },
    function(_e, _r, _body) {
      // console.log("EBM E: " + _e);
      // console.log("EBM R: " + util.inspect( _r, false, null) );
      // console.log("EBM R: " + _r);
      // console.log("EBM body: " + _body);

      _body = _body.trim().toLowerCase();
      _body = {
        response: _body,
        timestamp: +new Date()   
      }

      console.log( "_body: " + _body);

      if (_body.response == 'ok') {
        console.log('E-mail successfuly sent');
        res.jsonp(_body);
        //res.redirect("/thankyou");
        return;
      } else if (_body.response.indexOf('err:auth') > -1) {
        res.jsonp(_body);
        return;
    } else {
        _body.dmg_info = 'other type of error';
      }
    }
  ); 
}

```


```

function cheetah_renew(req, res) {
  // console.log('Renewing cookie');
  //Error: Hostname/IP doesn't match certificate's altnames
  //Solution: process.env.NODE_TLS_REJECT_UNAUTHORIZED = "0";
  //https://trig.cm.directv.com/api/login1?name=lex_api&cleartext=Ch33tah1

  //Call API Login
  request.get(
    { //Call API Login
      uri: 'https://ebm.cheetahmail.com/api/login1',
      qs: {
        "name" : "lex_api",
        "cleartext" : "Ch33tah1"
      }
    }, 
    function(_e, _r, _body) {
      // console.log("E: " + _e);
      // console.log("R: " + _r);
      // console.log("body: " + _body);  
      _body = _body.trim().toLowerCase();
      _body = {
          response: _body,
          form: req.body,
          timestamp: +new Date()
      }

      //Uncomment to simulate bad creds
      //_body.response = 'err:auth';

      if (_body.response == 'err:auth') {
        
        console.log('Maybe bad credentials? FATAL Error');
        _body.dmg_info = 'Bad Credentials';
      
      } else if (_r.headers['set-cookie'] && _body.response == 'ok') {
          
          console.log( _r.headers['set-cookie'] );

          cookie = _r.headers['set-cookie'];
         
          if (typeof cookie === 'object' && cookie.length === 1){
            cookie = cookie[0];
          }

          console.log('Authenticated, Cookie: ' + cookie);
          send_to_cheetah(req, res);
          return;

      } else {
          console.log('Authentication happened but headers or body was wrong.')
          _body.dmg_info = 'Authentication happened but headers or body was wrong.';
      }
    }
  );
}

```

