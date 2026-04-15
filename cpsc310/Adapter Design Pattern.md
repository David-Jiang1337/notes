The adapter design pattern is a pattern where incompatible types that nonetheless need to be used together are wrapped via an adapter class that holds a reference to each incompatible type and exposes methods for manipulating that type which are more conducive to the client's needs.

For instance, a music player that uses multiple different, incompatible libraries for different codecs might look like this:

![[adapterExample.png]]