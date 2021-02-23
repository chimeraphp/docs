# What's Chimera?

Chimera is a set of extensible components that leverage the [PSRs] to operate as a "glue framework".

That means your code won't be running using a home-brewed routing system or dependency injection container.
Instead, we have adapters for stable and battle-test libraries that are mixed together to create your software - ergo the name _Chimera_[^1]. 

The main motivation for taking this approach is that we already have several libraries and frameworks in the world.
However, most of them force you to structure your code in a certain way or directly depend on their components.

That's where we deviate.
We want everyone to be able to create software with minimal coupling to the libraries they choose and have the possibility to effortlessly move to other solutions - if/when that's needed.

Chimera puts you on the driving seat, giving you the freedom to define the organisation of your project and focus on your domain.

## License

The project and all its components are licensed under the MIT license.

[PSRs]: https://www.php-fig.org/psr/

[^1]: The term Chimera (_/kɪˈmɪərə/_ or _/kaɪˈmɪərə/_) has come to describe any mythical or fictional animal with parts taken from various animals, or to describe anything composed of very disparate parts, or perceived as wildly imaginative, implausible, or dazzling.
