# 7.2 // Generalização, Especialização e Polimorfismo // Lord of The Rings

Use este link do GitHub Classroom para ter sua cópia alterável deste repositório: <>

Implementar respeitando os fundamentos de Orientação a Objetos.

**Tópicos desta atividade:** generalização, super classes, classes abstratas, especialização, classes concretas e polimorfismo.

---

Fellowship of The Ring. Implementar a _Sociedade do Anel_, usando relacionamentos, herança, sobrecarga, comandos, consultas, etc, conforme os casos de teste a seguir.


```java
// Initializing People
Person Gandalf  = new Wizard("Gandalf");
Person Aragorn  = new Human("Aragorn");
Person Gimli    = new Dwarf("Gimli");
Person Legolas  = new Elf("Legolas");
Person Boromir  = new Human("Boromir");
Person Frodo    = new Hobbit("Frodo");
Person Sam      = new Hobbit("Sam");
Person Meriadoc = new Hobbit("Meriadoc");
Person Peregrin = new Hobbit("Peregrin");

// Initializing Fellowships
Fellowship FellowshipOfTheRing = new Fellowship("of The Ring");
Fellowship EvilFellowship      = new Fellowship("of Evil");

// Every person has a name
System.out.println(Gandalf.name().equals("Gandalf"));
System.out.println(Gandalf.toString().equals("Gandalf"));

// There is no members yet
System.out.println(FellowshipOfTheRing.toString().equals("Fellowship of The Ring"));
System.out.println(EvilFellowship.toString().equals("Fellowship of Evil"));
System.out.println(EvilFellowship.count() == 0);
System.out.println(FellowshipOfTheRing.count() == 0);
System.out.println(FellowshipOfTheRing.hasNoMembers() == true);
System.out.println(FellowshipOfTheRing.hasMembers() == false);

// Members count from 1 (not 0)
System.out.println(FellowshipOfTheRing.member(1) == null);
System.out.println(FellowshipOfTheRing.lastMember() == null);

// There is two members (order matters)
FellowshipOfTheRing.signUp(Gandalf); // member 1
FellowshipOfTheRing.signUp(Aragorn); // member 2
System.out.println(FellowshipOfTheRing.count() == 2);
System.out.println(FellowshipOfTheRing.hasNoMembers() == false);
System.out.println(FellowshipOfTheRing.hasMembers() == true);

// Member is a intermediary class between Fellowship and Person
System.out.println(FellowshipOfTheRing.member(1) instanceof Member);
System.out.println(FellowshipOfTheRing.member(2) instanceof Member);

// Through Member we can access the people
System.out.println(FellowshipOfTheRing.member(1).person().name().equals("Gandalf"));
System.out.println(FellowshipOfTheRing.member(1).person().equals(Gandalf));
System.out.println(FellowshipOfTheRing.member(1).person().equals(new Wizard("Gandalf")));
System.out.println(!FellowshipOfTheRing.member(1).person().equals(Aragorn));
System.out.println(FellowshipOfTheRing.member(2).person().equals(Aragorn));

// Out of Range should not throw an exception
System.out.println(FellowshipOfTheRing.member(-1) == null);
System.out.println(FellowshipOfTheRing.member(3) == null);

// The relationship is bidirectional
System.out.println(Aragorn.fellowship() == FellowshipOfTheRing);
System.out.println(Aragorn.fellowship() != EvilFellowship);
System.out.println(Aragorn.fellowship() == Gandalf.fellowship());
System.out.println(Gimli.fellowship() == null);

System.out.println(Aragorn.isMemberOfAFellowship() == true);
System.out.println(Aragorn.isMemberOfTheFellowship(FellowshipOfTheRing) == true);
System.out.println(Aragorn.isMemberOfTheFellowship(EvilFellowship) == false);
System.out.println(Gimli.isMemberOfAFellowship() == false);
System.out.println(Gimli.isMemberOfTheFellowship(FellowshipOfTheRing) == false);
System.out.println(Gimli.isMemberOfTheFellowship(EvilFellowship) == false);

// However, a person can be member of only one fellowship
EvilFellowship.signUp(Aragorn); // Aragorn has not been included
System.out.println(EvilFellowship.count() == 0);
System.out.println(EvilFellowship.hasNoMembers() == true);
System.out.println(Aragorn.fellowship() == FellowshipOfTheRing);
System.out.println(Aragorn.isMemberOfTheFellowship(FellowshipOfTheRing) == true);
System.out.println(Aragorn.isMemberOfTheFellowship(EvilFellowship) == false);

// There is another way to join the fellowships
Gimli.join(FellowshipOfTheRing);
Gimli.join(EvilFellowship); // has no effect (already in a fellowship)
System.out.println(FellowshipOfTheRing.count() == 3);
System.out.println(FellowshipOfTheRing.member(3).person().equals(Gimli));

// Even indirect way
Legolas.join(Gimli.fellowship());
System.out.println(FellowshipOfTheRing.count() == 4);
System.out.println(FellowshipOfTheRing.lastMember().person().equals(Legolas));

// More queries
System.out.println(FellowshipOfTheRing.count("Human") == 1);
System.out.println(FellowshipOfTheRing.count("Elf") == 1);
System.out.println(FellowshipOfTheRing.count("Hobbit") == 0);
System.out.println(FellowshipOfTheRing.has("Human") == true);
System.out.println(FellowshipOfTheRing.has("Hobbit") == false);

// Get the fellowship complete (adding various members at one time)
System.out.println(FellowshipOfTheRing.count() == 4);
FellowshipOfTheRing.signUp(Boromir, Frodo);
FellowshipOfTheRing.signUp(Sam, Meriadoc, Peregrin);
System.out.println(FellowshipOfTheRing.count() == 9);
System.out.println(FellowshipOfTheRing.count("Hobbit") == 4);

// Left the FellowshipOfTheRing
System.out.println(FellowshipOfTheRing.count() == 9);
System.out.println(FellowshipOfTheRing.count("Human") == 2);
System.out.println(Boromir.fellowship() == FellowshipOfTheRing);
System.out.println(FellowshipOfTheRing.member(5).person() == Boromir);

FellowshipOfTheRing.cancel(Boromir);

System.out.println(FellowshipOfTheRing.count() == 8);
System.out.println(FellowshipOfTheRing.count("Human") == 1);
System.out.println(Boromir.fellowship() == null);
System.out.println(FellowshipOfTheRing.member(5).person() == Frodo);

// Other way to unsubscribe
Frodo.left(); // leave current fellowship if any
System.out.println(FellowshipOfTheRing.count() == 7);
System.out.println(Frodo.fellowship() == null);

Gandalf.die();
System.out.println(FellowshipOfTheRing.count() == 6);
System.out.println(Gandalf.fellowship() == null);

// People can't join fellowships after die
System.out.println(FellowshipOfTheRing.count() == 6);
Gandalf.join(FellowshipOfTheRing);
System.out.println(Gandalf.fellowship() == null);
System.out.println(FellowshipOfTheRing.count() == 6);

// Asking if people are sharing a fellowship
System.out.println(Meriadoc.isFellowOf(Peregrin) == true);
System.out.println(Meriadoc.isFellowOf(Gandalf) == false);
System.out.println(Meriadoc.isFellowOf(Boromir) == false);
System.out.println(Meriadoc.isFellowOf(Meriadoc) == true);
System.out.println(Gandalf.isFellowOf(Gandalf) == true);

// Should be reflexive
System.out.println(Meriadoc.isFellowOf(Peregrin) == Peregrin.isFellowOf(Meriadoc));
System.out.println(Meriadoc.isFellowOf(Boromir) == Boromir.isFellowOf(Meriadoc));

// Yet another way to join a fellowship
System.out.println(Boromir.fellowship() == null);
Boromir.fellow(Meriadoc);
System.out.println(Boromir.fellowship() == Meriadoc.fellowship());
System.out.println(Meriadoc.isFellowOf(Boromir) == true);
Boromir.left();
System.out.println(Boromir.fellowship() == null);
Meriadoc.fellow(Boromir);
System.out.println(Boromir.fellowship() == Meriadoc.fellowship());

// Dissolve the fellowship :(
FellowshipOfTheRing.dissolve();
System.out.println(FellowshipOfTheRing.count() == 0);
System.out.println(FellowshipOfTheRing.hasNoMembers() == true);
System.out.println(FellowshipOfTheRing.member(1) == null);
System.out.println(FellowshipOfTheRing.lastMember() == null);
```
