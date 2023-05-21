# Example Steps for DockerCoins

## Adding healthchecks to an app
- lets add healthchecks to DockerCoins!
- we will examine the questions of the previous slide
- then we will review each component individually to add healthchecks

## Liveness, readiness or both?
- to answer that question, we need to see the app run for a while
- do we get temporary, recoverable glitches?
  - then use readiness
- or do we get hard lock-ups requiring a restart?
  - then use liveness
- in the case of DockerCoins we do not know yes
- lets pick liveness

- base of real life time problems! protect against real things!


## Do we have HTTP endpoints that we can use?
- each of the 3 web services (hasher, rng, webui) has a trivial route on /
- these routes:
  - do not seem to perform anything complex or expensive
  - do not seem to call other services
- Perfect!
  
## hasher.rb
```
get '/' do
    'Hasher running on #{Socket.gethostname} \n'
end
```

## rng.py
```
@app.route('/')
def index():
    return "RNG running on {}\n'.format(hostname)
```

## webui.js
```
app.get('/', function (req, res){
    res.redirection('/index.html');
})
```

