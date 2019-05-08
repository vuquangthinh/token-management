


# HOW IT WORK

```
import TokenManagement from './injectToken';

// test
let time = 1;

const tmn = new TokenManagement({
  isTokenValid(token) {
    if (time === 1) {
      ++time;
      return false;
    }

    return false;
  },
  getAccessToken() {
    return localStorage.getItem('accessToken');
  },
  onRefreshToken(done) {
    // call refresh token api

    console.log('----------------------------');
    console.log('refreshing');
    console.log('----------------------------');

    window.xz = () => done(12);
  },
});

export function injectToken(service) {
  return tmn.inject(service);
}


const testService = async token => {
  console.log('----------------------------');
  console.log('ok');
  console.log('----------------------------');

  return 'otken' + token;
};

const newInj = injectToken(testService);

(async () => {
  const [ val ] = await Promise.all([
    newInj(),
    newInj(),
    newInj(),
    newInj(),
    newInj(),
  ]);
  console.log('----------------------------');
  console.log(val, 'xyz');
  console.log('----------------------------');
})();


```