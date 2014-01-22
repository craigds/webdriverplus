.. _inspection:

Inspection & Manipulation
=========================

.. note::

    Some changes to be made here - slim down the number of methods,
    be more consistent.

.css(name, value)
------

A jQuery style shortcut to getting/setting ``css`` value of the element. Note
that name is javascript-style name (so ``backgroundColor`` instead of ``background-color``).
Leaving ``value`` empty will simply return the value of that css property.

.style
------

Returns an object that lets you get and set the CSS style of an element.

.. code-block:: python

    >>> import webdriverplus
    >>> driver = webdriverplus.Firefox()
    >>> driver.get('http://www.google.com')
    >>> for elem in driver.find('input'):
    >>>     elem.style.background = 'green'
    >>> driver.find('body').style.background = 'red'

.size
-----

Returns the size of the element, as a ``namedtuple``.

    >>> elem.size
    Size(width=300, height=25)
    >>> width, height = elem.size
    >>> width = elem.size.width

.location
---------

Returns the location of the element in the canvas, as a ``namedtuple``.

    >>> elem.location
    Location(x=10, y=50)
    >>> x, y = elem.location
    >>> x = elem.location.x
    >>> y = elem.location.y

.value
------

.type
-----

.name
-----

.is_checked()
-----------

Returns ``True`` if the checkbox has a ``checked`` attribute, ``False`` otherwise.

    >>> from webdriverplus import WebDriver
    >>> snippet = """
    ... <input type="checkbox" name="vehicle" value="Walk" />I walk to work</input>
    ... <input type="checkbox" name="vehicle" value="Cycle" checked />I cycle to work</input>
    ... <input type="checkbox" name="vehicle" value="Drive" />I drive to work</input>
    ... """
    >>> driver = WebDriver().open(snippet)
    >>> driver.find(value='Walk').is_checked
    False
    >>> driver.find(value='Cycle').is_checked
    True

.is_selected()
------------

Returns ``True`` if the option has a ``selected`` attribute, ``False`` otherwise.

    >>> from webdriverplus import WebDriver
    >>> snippet = """
    ... <select>
    ...     <option selected>Walk</option>
    ...     <option>Cycle</option>
    ...    <option>Driver</option>
    ... </select>
    ... """
    >>> driver = WebDriver().open(snippet)
    >>> driver.find(text='Walk').is_selected
    True
    >>> driver.find(text='Cycle').is_selected
    False

.is_enabled()
-----------

.is_displayed()
-------------

.class
------

Returns the set of CSS classes applied on the element.

.has_class(cls)
------

Checks if class ``cls`` is in the list of the element's classes

.id
---

Returns the 'id' attribute of the element.

.tag_name
---------

Returns the element's tag name.  (Eg. 'h1', 'div', 'input')

.attr(attribute)

Returns the ``attribute`` from the element with corresponding name

.attributes
-----------

Returns a dictionary-like object representing all the DOM attributes on the
element.  Supports getting, setting, and deleting attributes.

    >>> elem = driver.find(id='logo')
    >>> elem.attributes
    {u'width': u'50px', u'src': u'/static/images/logo.png', u'height': u'50px'}
    >>> elem.attributes['src']
    u'/static/images/logo.png'
    >>> elem.attributes['src'] = '/static/images/other.png'
    >>> del(elem.attributes['width'])
    >>> del(elem.attributes['height'])
    >>> elem.attributes
    {u'src': u'/static/images/other.png'}

.. note::

    The values returned by ``.attributes`` differ slightly from those
    returned by WebDriver's ``.get_attribute()``.

    Eg: When dealing with sizes, ``.attribute['height']`` returns a value like
    ``50px`` where ``.getAttribute('height')`` returns a value like ``50``.
    When dealing with links, ``.attribute['src']`` returns the raw src value,
    where ``.getAttribute('src')`` returns an absolute URL.

    Both styles are supported by WebDriver Plus.
