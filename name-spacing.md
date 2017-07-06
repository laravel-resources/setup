# useful reading (source: https://daylerees.com/code-smart-namespaces/)

In version 5.3 of PHP, a new feature known as name-spacing was added to the language. Many modern languages already had this feature for some time, but PHP was a little late to the scene. None the less, every new feature has a purpose. Let’s find out why PHP namespaces can benefit our application.

You can’t have two classes that share the same name. They have to be unique. The issue with this restriction is that if you are using a third party library which has a class named User, then you can’t create your own class also called User. This is a real shame because that’s a pretty convenient class name, right?

PHP namespaces allow us to circumvent this issue. In fact, we can have as many User classes as we like. Not only that, but we can use namespaces to contain our similar code into neat little packages, or even to show ownership.

Let’s take a look at a normal class. Yes. I know you have used them before. Just trust me on this one, okay?

Global Namespace

Here’s a simple class.

<?php

// app/Eddard.php

class Eddard
{

}
There’s nothing special about it. If we want to use it then, we can do this.

<?php

// app/Http/routes.php

$eddard = new Eddard;
Dayle, I know some PHP...

Okay, okay. Sorry.

We can think of this class as being in the 'global' namespace. I don’t know if that’s the right term for it, but it sounds quite fitting to me. It essentially means that the class exists without a namespace. It’s just a normal class.

Simple Name-spacing

Let’s create another class alongside the original, global Eddard.

<?php

namespace Stark;

// app/another.php

class Eddard
{

}
Here we have another Eddard class, with one minor change. The addition of the namespace directive. The line namespace Stark; informs PHP that everything we do is relative to the Stark namespace. It also means that any classes created within this file will live inside the ‘Stark’ namespace.

Let's try to use the ‘Eddard’ class once again.

<?php

// app/Http/routes.php

$eddard = new Eddard;
Once again, we get an instance of the first class we created in the last section. Not the one within the ‘Stark’ namespace. Let’s try to create an instance of the ‘Eddard’ within the ‘Stark’ namespace.

<?php

// app/Http/routes.php

$eddard = new Stark\Eddard;
We can instantiate a class within a namespace, by prefixing it with the name of the namespace, and separating the two with a backward (\) slash. Now we have an instance of the ‘Eddard’ class within the ‘Stark’ namespace. Aren’t we magical?!

You should know that namespaces can have as many levels of hierarchy as they need to. For example.

This\Namespace\And\Class\Combination\Is\Silly\But\Works
The Theory of Relativity

Remember how I told you that PHP always reacts relative to the current namespace? Well, let’s take a look at this in action.

<?php

namespace Stark;

// app/Http/routes.php

$eddard = new Eddard;
By adding the namespace directive to the instantiation example, we have moved the execution of the PHP script into the ‘Stark’ namespace. Since we are inside the same namespace as the one we put ‘Eddard’ into, we receive the name-spaced ‘Eddard’ class. See how it’s all relative?

Now that we have changed the active namespace, we have created a little problem. Can you guess what it is? How do we instantiate the original ‘Eddard’ class? The one not in the namespace.

Fortunately, PHP has a trick for referring to classes that are located in the global namespace. We simply prefix them with a backward (\) slash.

<?php

// app/Http/routes.php

namespace Stark;

$eddard = new \Eddard;
With the leading backward (\) slash, PHP knows that we are referring to the ‘Eddard’ in the global namespace, and instantiates that one.

Use your imagination a little, like how Barney showed you. Imagine that we have another namespaced class called Tully\Edmure. Now we want to use this class from within the ‘Stark’ framework. How do we do that?

<?php

namespace Stark;

// app/Http/routes.php

$edmure = new \Tully\Edmure;
One again, we need the prefixing backward slash to bring us back to the global namespace before instantiating a class from the ‘Tully’ namespace.

It could get tiring referring to classes within other namespaces by their full hierarchy each time. Luckily, there’s a nice little shortcut we can use. Let’s see it in action.

<?php

namespace Stark;

use Tully\Edmure;

// app/Http/routes.php

$edmure = new Edmure;
Using the use statement, we can bring one class from another namespace into the current namespace. This will allow us to instantiate it by name only.

We can give our imported classes little nicknames like we used to in the PHP playground. Let me show you.

<?php

namespace Stark;

use Tully\Brynden as Blackfish;

// app/Http/routes.php

$edmure = new Blackfish;
By using the ‘as` keyword, we have given our ‘Tully/Brynden’ class the ‘Blackfish’ nickname. This will allow us to use the new nickname to identify it within the current namespace. Neat trick, right? It’s also really handy if you need to use two similarly named classes within the same namespace. For example.

<?php

namespace Targaryen;

use Dothraki\Daenerys as Khaleesi;

// app/Http/routes.php

class Daenerys
{

}

// Targaryen\Daenerys
$daenerys = new Daenerys;

// Dothraki\Daenerys
$khaleesi = new Khaleesi;
By giving the ‘Daenerys’ within the ‘Dothraki’ namespace a nickname of ‘Khaleesi’, we can use two ‘Daenerys’ classes by name only. Handy, right? The game is all about avoiding conflicts and grouping things by purpose or faction.

You can use as many classes as you need to.

<?php

namespace Targaryen;

use Stark\Eddard;
use Lannister\Tyrion;
use Dothraki\Daenerys;
use Snow\Jon as Bastard;
Structure

Namespaces aren’t just about avoiding conflicts. We can also use them for organization and ownership. Let me explain with another example.

Let’s say I want to create an open source library. I’d love for others to use my code; it would be great! The trouble is, I don’t want to cause any problematic class name conflicts for the person using my code. That would be terribly inconvenient. Here’s how I could avoid causing hassle for the wonderful, open source embracing, individual.

Dayle\Blog\Content\Post
Dayle\Blog\Content\Page
Dayle\Blog\Tag
Here we have used my name to show that I created the original code, and to separate my code from that of the person using my library. Inside the base namespace, I have created some sub-namespaces to organize my application by its internal structure.

In the composer section, you will learn how to use namespaces to simplify the act of loading class definitions. I strongly suggest you take a look at this useful mechanism.

Limitations

In truth, I feel a little guilty for calling this sub-heading ‘Limitations.' What I’m about to talk about isn’t a bug.

You see, in other languages, namespaces are implemented in a similar way. Those other languages provide an additional feature when interacting with namespaces.

In Java, for example, you can import some classes into the current namespace by using the import statement with a wildcard. In Java, ‘import’ is equivalent to ‘use’, and it uses dots to separate the nested namespaces (or packages). Here’s an example.

import dayle.blog.*;
The above would import all of the classes that are located within the ‘dayle.blog’ package.

In PHP, you simply can’t do that. You have to import each class individually. Sorry about that. Actually, why am I saying sorry? Go and complain to the PHP internals team instead. Only, be gentle. They have given us a lot of cool stuff recently.

Here’s a neat trick you can use. Imagine that we have this namespace and class structure, as in the previous example.

Dayle\Blog\Content\Post
Dayle\Blog\Content\Page
Dayle\Blog\Tag
We can give a sub-namespace a nickname, to use it’s child classes. Here’s an example.

<?php

namespace Baratheon;

use Dayle\Blog as Cms;

// app/Http/routes.php

$post = new Cms\Content\Post;
$page = new Cms\Content\Page;
$tag  = new Cms\Tag;
This should prove useful if you need to use many classes within the same namespace. Enjoy!
