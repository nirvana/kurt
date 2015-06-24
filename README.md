# kurt
You're so vain, you probably think this repo is about you... about you...

### What is kurt?

Most simply, Kurt is a general purpose UI.  More concretely, it is an open source Unity Application,
and library, that when compiled produces a client for a web service.  This client creates a UI using
all of the power of the Unity game engine!  Even more concretely, a server speaks JSON back and forth
with the client, the JSON describes pages in an application, and Kurt uses it to render the UI, and
from that UI collect UI events (like button presses) which are sent back to the server (Again as JSON)

Thus instead of building a web app on the backend, you build a REST API that speaks a predefined JSON
language, which Kurt renders into graphics.

This can run in the browser as a WebGL context, or via Unity's build system produce native apps for
mobile and the desktop.

### Challenges:

  1. Define the library.  Eventually others will want to make derivatives of kurt to give specific
  functionality on the client side, this project serves as an example of what can be done, but also
  a library of pre-created functionality (UI Widgets) for them to work from.  Those widgets need to
  be specified, both their JSON representation and the variables that can be changed, along with C#
  code to serve as a base implementation.  

  Note: The entire UI is represented by a single JSON object that has as sub-objects all of the
  widgets.  EG: a button is on a card which is on a scrollview. This is exactly like the view
  hierarchy in iOS UIViews.  You can accomplish this in Unity by creating an object hierarchy that
  mirrors exactly the JSON hierarchy.

    For example, a KTButton might look like this in JSON:
    ```
    {
      "type" : "KTButton",
      "id" : "button22"
      "location" : { "x" : 1, "y": 2, "z" : 3},
      "size" : {"width" : 123, "height" : 12.3},
      "events" : {
        "onRelease" : "/someapp/button22/released"
      }
    }
    ```

  Thus your deliverable is a generic kurt renderer written in Unity (so a Unity project) and the
  description/documentation/specification of Kurt UI Widgets.

  I *strongly* recomend doing a complete pass on this with the minimal UI set, maybe just one. And
  then expand it with more widgets over time.

  2. Build a simple application to render each of the objects in the library. So for the above button,
  the app would create a button at the specified location and size and when it was pressed, on release,
  the event would be sent to the given REST endpoint

  3. Build a theming system.  This needs to happen at the same time as the above two steps.  So, for
  a given site a theme can be described (again in JSON) which adjusts colors, uses images for parts
  of things (like the top border of a box, etc).   This way UIs can be built for applications that
  are later customized via theming by clients (Eg: the way a tumbler them changes your tumbl)

  When you render (or create?) and object in C# from the JSON, fold in the theme as part of that step.

  4. Suggested components and order to build them:
    - Background View - scrollable, vertically or horizontally.  All other widgets will go in this
    view hierarchically.
    - Card view - Cards are the new UI hotness.  
    - Label Field - Text that you can't edit
    - Buttons
    - Text Field - Text that you can edit

  5. All we're doing at this stage is making a demo of what can be done. Things don't need to be
  super flexible.  You can push some JSON pages to S3 or github pages as a proxy for the server,
  and have the client just pull those pages and render them (eg: one page as the UI an other as the
  theme.)

  6. We also need to build a fallback for older browsers taht don't support WebGL.  This would be
  code (in Elixir) that takes the above JSON UI and Theme descriptions and renders out an HTML/CSS
  page from them. This will also serve as the SEO view for crawlers like googlebot.

## Resources:

Unity: http://unity3d.com -- Just get the free version of Unity that's fine for our needs.

Our design aesthetic is flat, simple and clean.  Think Apple, not Google matierals.
