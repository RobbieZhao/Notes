## mux.go
 
    type Router struct {
        // Configurable Handler to be used when no route matches.
        // This can be used to render your own 404 Not Found errors.
        NotFoundHandler http.Handler
            
        // Configurable Handler to be used when the request method does not match the route.å
        // This can be used to render your own 405 Method Not Allowed errors.
        MethodNotAllowedHandler http.Handler
            
        // Routes to be matched, in order.
        routes []*Route
            
        // Routes by name for URL building.
        namedRoutes map[string]*Route
            
        // If true, do not clear the request context after handling the request.
        //
        // Deprecated: No effect, since the context is stored on the request itself.
        KeepContext bool
            
        // Slice of middlewares to be called after a match is found
        middlewares []middleware
            
        // configuration shared with `Route`
        routeConf
    }
    
    // common route configuration shared between `Router` and `Route`
    type routeConf struct {
        // If true, "/path/foo%2Fbar/to" will match the path "/path/{var}/to"
        useEncodedPath bool
            
        // If true, when the path pattern is "/path/", accessing "/path" will
        // redirect to the former and vice versa.
        strictSlash bool
            
        // If true, when the path pattern is "/path//to", accessing "/path//to"
        // will not redirect
        skipClean bool
            
        // Manager for the variables from host and path.
        regexp routeRegexpGroup
            
        // List of matchers.
        matchers []matcher
            
        // The scheme used when building URLs.
        buildScheme string
    
        buildVarsFunc BuildVarsFunc
    }
    
    func NewRouter() *Router
    
    func (r *Router) Match(req *http.Request, match *RouteMatch) bool
    
    func (r *Router) ServeHTTP(w http.ResponseWriter, req *http.Request)
    
    // Get returns a route registered with the given name.
    func (r *Router) Get(name string) *Route

### Setters set router configurations

    func (r *Router) StrictSlash(value bool) *Router
    
    func (r *Router) SkipClean(value bool) *Router
    
    func (r *Router) UseEncodedPath() *Router
    
### Getters 
    // Get returns a route registered with the given name.
    func (r *Router) Get(name string) *Route

### Context

    // RouteMatch stores information about a matched route.
    type RouteMatch struct {
        Route   *Route
        Handler http.Handler
        Vars    map[string]string
            
        // MatchErr is set to appropriate matching error
        // It is set to ErrMethodMismatch if there is a mismatch in
        // the request method and route method
        MatchErr error
    }


### Route factories 

These functions essentially just make a new route and pass down the parameters

    // NewRoute registers an empty route.
    func (r *Router) NewRoute() *Route
    
    // Name registers a new route with a name.
    // See Route.Name().
    func (r *Router) Name(name string) *Route
    
    // Handle registers a new route with a matcher for the URL path.
    // See Route.Path() and Route.Handler().
    func (r *Router) Handle(path string, handler http.Handler) *Route
    
    // HandleFunc registers a new route with a matcher for the URL path.
    // See Route.Path() and Route.HandlerFunc().
    func (r *Router) HandleFunc(path string, f func(http.ResponseWriter, *http.Request)) *Route
    
    // Headers registers a new route with a matcher for request header values.
    // See Route.Headers().
    func (r *Router) Headers(pairs ...string) *Route
    
    // Host registers a new route with a matcher for the URL host.
    // See Route.Host().
    func (r *Router) Host(tpl string) *Route

    // MatcherFunc registers a new route with a custom matcher function.
    // See Route.MatcherFunc().
    func (r *Router) MatcherFunc(f MatcherFunc) *Route

    // Methods registers a new route with a matcher for HTTP methods.
    // See Route.Methods().
    func (r *Router) Methods(methods ...string) *Route
    
    // Path registers a new route with a matcher for the URL path.
    // See Route.Path().
    func (r *Router) Path(tpl string) *Route 

    // PathPrefix registers a new route with a matcher for the URL path prefix.
    // See Route.PathPrefix().
    func (r *Router) PathPrefix(tpl string) *Route

    // Queries registers a new route with a matcher for URL query values.
    // See Route.Queries().
    func (r *Router) Queries(pairs ...string) *Route

    // Schemes registers a new route with a matcher for URL schemes.
    // See Route.Schemes().
    func (r *Router) Schemes(schemes ...string) *Route

    // BuildVarsFunc registers a new route with a custom function for modifying
    // route variables before building a URL.
    func (r *Router) BuildVarsFunc(f BuildVarsFunc) *Route

    // Walk walks the router and all its sub-routers, calling walkFn for each route
    // in the tree. The routes are walked in the order they were added. Sub-routers
    // are explored depth-first.
    func (r *Router) Walk(walkFn WalkFunc) error 



## middleware.go

    type MiddlewareFunc func(http.Handler) http.Handler
## route.go


    // Route stores information to match a request and build URLs.
    type Route struct {
        // Request handler for the route.
        handler http.Handler
        // If true, this route never matches: it is only used to build URLs.
        buildOnly bool
        // The name used to build URLs.
        name string
        // Error resulted from building a route.
        err error
            
        // "global" reference to all named routes
        namedRoutes map[string]*Route
            
        // config possibly passed in from `Router`
        routeConf
    }

### Getter

    func (r *Route) SkipClean() bool
    func (r *Route) GetError() error
    func (r *Route) GetHandler() http.Handler
    func (r *Route) GetName() string
    
### Setter

    func (r *Route) BuildOnly() *Route
    func (r *Route) Handler(handler http.Handler) *Route {
    func (r *Route) HandlerFunc(f func(http.ResponseWriter, *http.Request)) *Route
    func (r *Route) Name(name string) *Route
	