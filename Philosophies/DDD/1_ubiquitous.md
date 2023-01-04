# The Ubiquitous Language

The developers think differently from the domain experts. The devs think of object classes, the relationship between them in terms of inheritance, polymorphism, OOP, etc. And they may solve real world problems by associating components with code. But the domain experts know nothing about that, and they have their own jargon.

To overcome this difference in communication style, when we build the model, we must communicate to exchange ideas about the moedl, about the elements involved in the model, how we connect them, what is relevant and what is not.

A core principle of DDD is to use a language based on the model. The model is the common ground. Use it as the backbone of a language. Request that the team use the language consistently in all communications, and also in the code. Make sure this language appears consistently in all communication forms used by the team; hence the name "*The Ubiquitous Language*".

## Creating the Ubiquitous Language

Here is a hypothetical dialog between a software developer and a domain expert in the air traffic monitoring project.

**Dev** : We want to monitor air traffic. Where do we start?

**Expert** : Let's start with the basics. All this traffic is made up of **planes**. Each plane takes off from a **departure** place, and lands at a **destination** place.

**Dev** : When it flies, the plan can just choose any air path the pilots like? As long as they reach the destination?

**Expert** : No, they receive a **route** they must follow. And should stay on that route as close as possible.

**Dev** : I'm thinking of this **route** as a 3D path in the air. We can use Cartesian system of coordinates, then the route is simply a series of 3D coordinates.

**Expert** : No. The **route** is actually the projection on the ground of the expected air path of the plane. The series of points on the ground are determined by their **latitude** and **longitude**

**Dev** : Ok, then let's call each of those points a **fix**. We'll use a series of 2D points to describe the path. Then the **departure** and **destination** are just one of those **fixes**. The plane must then follow the route but does that mean that it can fly as high or as low as it likes?

**Expert** : No. The **altitude** than an airplane is to have at a certain moment is also established in the **flight plan**.

**Dev** : **Flight plan**? Sounds important. What is that?

**Expert** : Before leaving the airport, the pilots receive a detailed **flight plan** which includes all sorts of information about the **flight**: the **route**, cruise **altitude**, cruise **speed**, type of **airplane**, even information about the crew memebers.

.... and so on

