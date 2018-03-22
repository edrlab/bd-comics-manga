# Technical decisions

## Descriptive approach
Effects like transitions may be defined as Javascript code, like Jake Archibald's proposal expressed in [Navigation Transitions](https://github.com/jakearchibald/navigation-transitions).

In such case, we would need to define effects, their parameters, and their Javascript implementation (JS being the lingua franca of Web application).

But several important facts stop us tu use this path:
1. This WG would need to be prescriptive on the best implementation of the different effects in Javascript. We are certainly not the best JS developers in the world.   
2. To embed javascript in an ebook is doomed for any preservation purpose. Javascript is evolving too quickly to expect that code written today will be readable with Web based toolkits in 30 years from now.
3. This would mean that authoring tools would have to generate this code automatically, from the effects described by ebooks authors in a user-friendly interface. The necessary evolutions of the code would then need to be applied to each authoring system at about the same time, which is almost impossible. 

Therefore the WG defines descriptive structures for each effect, easy to implement in authoring solutions. And ebook reading systems will implement each effect the best they can, in any language they want (depending the platform). 

## JSON-LD serialization
The structures describing the effects will be serialized as JSON-LD, like the [Readium-2 webpub manifest](https://github.com/readium/webpub-manifest) currently proposed as a base for the W3C Web Publication manifest.
