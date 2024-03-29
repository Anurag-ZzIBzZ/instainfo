.. meta::
   :description:
      Documentation of instainfo module, a powerful and intuitive
      Python library to download Instagram media and metadata.

.. _python-module-instainfo:

Python Module :mod:`instainfo`
--------------------------------

.. module:: instainfo

.. highlight:: python

instainfo exposes its internally used methods and structures as a Python
module, making it a powerful and intuitive Python API for Instagram,
allowing to further customize obtaining media and metadata.

Start with getting an instance of :class:`instainfo`::

    import instainfo

    # Get instance
    L = instainfo.instainfo()

    # Optionally, login or load session
    L.login(USER, PASSWORD)        # (login)
    L.interactive_login(USER)      # (ask password on terminal)
    L.load_session_from_file(USER) # (load session created w/
                                   #  `instainfo -l USERNAME`)

:mod:`instainfo` provides the :class:`Post` structure, which represents a
picture, video or sidecar (set of multiple pictures/videos) posted in a user's
profile. :class:`instainfo` provides methods to iterate over Posts from a
certain source::

    for post in instainfo.Hashtag.from_name(L.context, 'cat').get_posts():
        # post is an instance of instainfo.Post
        L.download_post(post, target='#cat')

:class:`Post` instances can be created with:

- :func:`Post.from_shortcode`
   Use a Post shortcode (part of the Post URL,
   ``https://www.instagram.com/p/SHORTCODE/``) to create a Post
   object::

      post = Post.from_shortcode(L.context, SHORTCODE)

- :meth:`Profile.get_posts`
   All media of a :class:`Profile`.

- :meth:`Profile.get_saved_posts`
   Media that the user marked as saved (:class:`Profile` must be own profile
   for this to work)

- :meth:`instainfo.get_feed_posts`
   Media in the user's feed.

- :meth:`instainfo.get_explore_posts`
   Media that is suggested by Instagram to explore.

- :meth:`Hashtag.get_posts`
   Media associated with given hashtag.

With the :class:`Profile` class, instainfo also makes it easy to access
metadata of a Profile. :class:`Profile` instances can be created with:

- :meth:`Profile.from_username`::

     profile = Profile.from_username(L.context, USERNAME)

- :meth:`Profile.from_id`
   given its User ID. This allows to easily lookup a Profile's username given
   its ID::

      Profile.from_id(L.context, USERID).username

- :meth:`Profile.get_followees`
   Profiles that are followed by given user.

- :meth:`Profile.get_followers`
   Profiles that follow given user.

- :attr:`Post.owner_profile`, :attr:`Story.owner_profile`, :attr:`StoryItem.owner_profile`
   Owner profile of particular object.

- :meth:`Post.get_likes`
   Profiles that liked a given :class:`Post`

- :attr:`PostComment.owner`
   Profile of a Post comment.

For a list of a few code examples that use the instainfo module, see
:ref:`codesnippets`.

The reference of the classes and functions provided by the :mod:`instainfo` module is
divided into the following subsections:

.. toctree::
   :maxdepth: 2

   module/instainfo
   module/structures
   module/nodeiterator
   module/instainfocontext
   module/exceptions
