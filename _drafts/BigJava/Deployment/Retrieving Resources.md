
# Retrieving Resources

Use the `getResource` method to read resources from a JAR file. For example, the following code retrieves images from a JAR file.

```

// Get current classloader
ClassLoader cl = this.getClass().getClassLoader();
// Create icons
Icon saveIcon  = new ImageIcon(cl.getResource("images/save.gif"));
Icon cutIcon   = new ImageIcon(cl.getResource("images/cut.gif"));

```

The example assumes that the following entries exist in the application's JAR file:

- images/save.gif
- images/cut.gif
