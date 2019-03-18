---
layout : post
title : 'Schablonen und Sichtbarkeit'
author : 'Michael Strassberger'
date : 2017-05-14 14:00
categories : se2 se2-2017
---

## Schablonen- und Einschubmethoden

Wiederholung:
* Schablonenmethoden definieren einen Rahmen mit Platzhaltern, die erst zu einen späteren Zeitpunkt gefüllt werden durch SubTypen. 
* Einschubmethoden werden genutzt um die Platzhalter in Schablonen zu füllen. 

Wir veranschaulichen uns das mal an einen Beispiel für ein einfachen Blog Eintrag:
{% highlight java linenos %}
public abstract class BlogPost
{
    public String getFormatedPost()
    {
        String post  = "<html>";
               post += "<head> <title>" + getTitle() + "</title></head>";
               post += "<body> <h1>" + getTitel() + "</h1>";
               post += "<p>" + getContent() + "</p>";
               post += "<span> Geschrieben von " 
                       + getAuthor() + "</span>";
               post += "</body> </html>";

        return post;
    }

    public abstract String getTitle();
    public abstract String getContent();
    public abstract String getAuthor();
}
{% endhighlight %}

* Z.3-13 Ist dabei unsere Schablone sie definiert den Aufbau unseres Blog Eintrages
* Z.15-17 Sind unsere Einschubmethoden.

Wenn wir nun einen Blog Eintrag erstellen wollen erben wir von Blog-Post und müssen nur die Einbschubmethoden implementieren. 

{% highlight java linenos %}
public class BlogPostTutorium extends BlogPost
{
    public String getTitle()
    {
        return "Tutorium vom 3. Mai 2017";
    }

    public String getContent()
    {
        return "Hello World";
    }

    public String getAuthor()
    {
        return "Michael";
    }
}
{% endhighlight %}

Wenn wir nun ein Exemplar von BlogPostTutorium erstellen und daran 'getFormatedPost' aufrufen erhalten wir als Rückgabe folgendes:

{% highlight html linenos %}
<html>";
<head> <title> Tutorium vom 3. Mai 2017</title></head>"
<body> <h1> Tutorium vom 3. Mai 2017 </h1>
<p>Hello World </p>
<span> Geschrieben von Michael</span>
</body> </html>
{% endhighlight %}

Das Beispiel stellt jetzt natürlich keine sinnvolle Modellierung eines Blogs dar. Dieses Beispiel sollte aber verdeutlichen wie das Schablonen- und Einschubmethoden Konzept benutzt werden kann um ein Grundgerüst zu deklarieren und es dann über einen Subtypen mit Inhalt zu füllen.


## Sichtbarkeitsmodifikatoren in Java

Mit der Einführung von Modulen (package) wird es Zeit sich mit dem Abstufungen der Restriktion von den in Java zur Verfügung gestellten Modifikatoren auseinanderzusetzen.

Modifikator | Sichtbarkeitsbereich (Scope)
private | Nur die direkte Klassen und seine Unterklassen habe darauf zugriff (nested class)
protected | " - " + SubTypen der Klasse die von ihr per 'extends' erben haben zugriff
default | " - " + Alle Klassen innerhalb des Moduls 'package' haben zugriff auf die Variable. Man spricht hier auch vom package private
public | Alle in dem Projekt befindlichen Klassen haben zugriff. Dies gilt auch für Klassen und Methoden außerhalb des Projektes.

Mit diesen Abstufungen können wir sehr genau unsere Sichtbarkeit von Klassen, variablen und Methoden definieren. Als Design Ansatz gilt dabei immer ***so wenig wie möglich, so viel wie nötig*** dadurch sorgen wir dafür das nach außen hin nur die für die Funktionalität wichtigen Methoden und Klassen sichtbar sind.


