# RazorForms.Bootstrap

This small package adds preconfigured Bootstrap support to RazorForms.

## How to use

There are two ways to use the Bootstrap configuration.

### Use default Bootstrap options

If you want to use the default options, all you have to do is replace your call to `services.UseRazorForms()` with a call to `services.UseRazorFormsWithBootstrap()`:

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();

// builder.Services.UseRazorForms();
builder.Services.UseRazorFormsWithBootstrap();
```

This adds some basic default classes to the RazorForms components. I don't recommend using default Bootstrap options in a production app because they're pretty basic, but it gets some basic Bootstrap styling set up so you can start developing your app.

### Customize the Bootstrap classes applied

If you want to customize the basic Bootstrap options (and you should), you can use the overload of `UseRazorFormsWithBootstrap()` that accepts an `Action<RazorFormsOptions>`. Mutate the options in place, and the result is added to dependency injection for use by RazorForms later.

Say you want to add a bottom margin around all input types. To do that:

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();
builder.Services.UseRazorFormsWithBootstrap(o => 
{
    o.InputOptions.ComponentWrapperClasses = "mb-3";
	o.CheckInputGroupOptions.ComponentWrapperClasses = "mb-3";
	o.RadioInputGroupOptions.ComponentWrapperClasses = "mb-3";
	o.TextAreaOptions.ComponentWrapperClasses = "mb-3";
	o.SelectOptions.ComponentWrapperClasses = "mb-3";
});
```

#### Preserving existing options

Sometimes, you want to add new classes to the existing classes. The simplest way to do this is using string interpolation. For example, to add a small margin to the error list without removing its default classes:

```csharp
using Microsoft.AspNetCore.Builder;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;

var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddRazorPages();
builder.Services.UseRazorFormsWithBootstrap(o => 
{
    o.InputOptions.ErrorWrapperClasses = $"{o.InputOptions.ErrorWrapperClasses} mt-1";
});
```

## Additional information

You still need to include the Bootstrap CSS yourself. All this package does is set up CSS class names.

For additional information on RazorForms and how it can be customized, see the [docs](https://www.razorforms.com).