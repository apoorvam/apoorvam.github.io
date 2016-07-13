---
layout: post
title:  "Get all the source folders in an eclipse project"
summary: Here is how to get all source directories in Java build path of an eclipse project
date:   2015-07-10 15:00:00 +0530
categories: eclipse java source
---

Do you want to get a list of all the source directories in an eclipse project?

The source directories can be more than one. They can also be linked to directories, present outside the eclipse project. This could be needed if you are doing Eclipse Plugin Development.

Below code snippet shows how to get a list of all the source directories, specified in Java Build Path:

{% highlight java %}
public ArrayList getAllSourceFolders() throws JavaModelException {
	ArrayList paths = new ArrayList();
	if (project.isOpen() && JavaProject.hasJavaNature(project)){
		IJavaProject javaProject = JavaCore.create(project);
		IClasspathEntry[] classpathEntries = javaProject.getResolvedClasspath(true);
		for(int i = 0; i<classpathEntries.length;i++) {
			IClasspathEntry entry = classpathEntries[i];
			if(entry.getEntryKind() == IClasspathEntry.CPE_SOURCE){
				paths.add(entry.getPath());
			}
		}
	}
	return paths;
}
{% endhighlight %}
