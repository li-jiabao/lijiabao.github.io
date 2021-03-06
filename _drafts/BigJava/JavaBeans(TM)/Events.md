
# Events

A bean class can fire off any type of event, including custom events. As with properties, events are identified by a specific pattern of method names.

```

public void add*&lt;Event&gt;*Listener(*&lt;Event&gt;*Listener a)
public void remove*&lt;Event&gt;*Listener(*&lt;Event&gt;*Listener a)

```

The listener type must be a descendant of `java.util.EventListener`.

For example, a Swing `JButton` is a bean that fires `action` events when the user clicks on it. `JButton` includes the following methods (actually inherited from `AbstractButton`), which are the bean pattern for an event:

```

public void addActionListener(ActionListener l);
public void removeActionListener(ActionListener l);

```

Bean events are recognized by builder tools and can be used in wiring components together. For example, you can wire a button's `action` event to make something happen, like invoking another bean's method.
