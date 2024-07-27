# Advertisement-Addon-for-BookStack
A Simple little addon to add advertisement to your BookStack based website.

COMING SOON... I WILL POST BookStack Reddit when is ready 

Just sharing my little changes to my BookStack

Open Conposer.json and find 
<pre><code>
        "files": [
            "app/App/helpers.php",
			//Add this line "app/Ads/Helpers/AdHelper.php"
        ]
</code></pre>
Open Kernel and Add

<pre><code>
protected $routeMiddleware = [
    // other middlewares
    'checkRole' => \BookStack\Http\Middleware\CheckRole::class,
];
</code></pre>

Open Route/web.php and add
<pre><code>
use BookStack\Ads\Controllers\AdsController;

// Apply the middleware to the routes, checkRole:1 is admin only
Route::group(['middleware' => ['checkRole:1']], function() {
    Route::get('/ads/create-ads', [AdsController::class, 'createAds'])->name('ads.ads');
    Route::post('ads/store-ads', [AdsController::class, 'storeAds'])->name('ads.storeAds');
</code></pre>

go to themes
resources/views/layouts/parts/header-links-start.blade.php
or 
themes/YourTheme/layouts/parts/header-links-start.blade.php 
and add the new menu 
 I did it like this 
<pre><code>
  @if(!user()->isGuest() && userCan('users-manage') && !userCan('settings-manage'))
        <a href="{{ url('/ads/create-ads') }}"
           data-shortcut="settings_view">@icon('users'){{ trans('settings.users') }}</a></code></pre>
    @endif


visit your site https://yoursite.com/ads/create-ads and your will find more instructions there
