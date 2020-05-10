# Angular_Routing

#### In production change the base href from '/' to '/APM'

ng build --base-href /APM/

####

paths are case sensitive.

order of the routes matters.router uses first match win strategy.so,more specific path should always be before less specific path

{path:'welcome',redirectTo:'home',pathmatch:'full'}

redirect route can't be changed to another redirect.

redirects can be local or absolute.above is local redirect.prefix of / is needed for absolute redirect

Use RouteModule.forRoot() for app routes (must be one time only)

Use RouteModule.forChild() for feature routes

since route order matters, forchild routes seen first.later forroot

#### '/welcome' > HTML5 urls (default) | "#/welcome' > hash based urls

for hash based urls use RouteModule.forRoot([...],{useHash:true})

####

if we use secondary routes inluding primary like '/products(popup:messages)' then unlike router.navigateByUrl, router.navigate keeps the secondary routes.

use navigateByUrl to ensure every existing route parameter & secondary route is removed.ex:we use it for logout route

#### route parameters

use '/products/:id/edit' for edit product page
use '/products/0/edit' for Add product page, because edit component can be reused

use this.route.snapshot.paramMap when we need to read parameter only once and it never changes

use this.route.paramMap.subscribe when we need to read changing parameter

#### optional route paramaters

defined in curly braces with key value.

optional route parameters must always be after required route parameters

#### Prefetching Data Using Route Resolvers

used to prevent partial page load due to time taken to retrive data.

using resolvers page is loaded only after the full data is retrieved.prevents display of partial page

prevent routing to page where there an error.improves flow when error occurs.

#### Route 'data' property in RouterModule.forChild

{path:'products',component:ProductListComponent,data:{pageTitle:'Product List'}}

this.route.snapshot.data['pageTitle']//no need to use observable since it cannot change through out the lifetime of app

used to provide any arbitrary data to a route.Data defined in 'data' property cannot change through out the lifetime of the application.so we use it for static data.Ex:pageTitle

#### child routes

to define routes within other routes.ie.to display routed component templates within other routed component template.

tabs/breadcrumbs are nice way to show child routes.

child routes can be used to build master/detail style page

child routes are required for lazy loading

Absolute path(begins with /) for child route::::<a [routerLink]="['/products',product.id,'edit','info']">Info</a>
::::this.router.navigate(['/products',this.product.id,'edit','info'])

Relative path(does not begins with /) for child route::::<a [routerLink]="['info']">Info</a>
::::this.router.navigate(['info'],{relativeTo: this.route})::::this.route is ActivatedRoute
