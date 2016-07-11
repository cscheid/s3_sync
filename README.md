# Simple directory syncing to s3 for static web hosting

If you're trying host a static website on Amazon's S3, you've likely
encountered a mix of "WHY WON'T S3 DO THE RIGHT THING WITH MY
MIMETYPES?!" and "WHY DOES AWSCLI INSIST ON REUPLOADING EVERYTHING
EVERYTIME?"

I'm as bewildered as you are. 

But here's a script that does the simple, obvious thing (noting that
simple and obvious is *not* what `aws` *or* `s3cmd` do). Throw this
thing into your `$PATH` and then:

    $ cd ${DIR_YOU_WANT_TO_SYNC}
	$ sync_with_s3.py ${S3_BUCKET_NAME}

It will: 

* upload things which are not in the bucket
* upload things that have a mismatched MD5 checksum
* remove things that are not on the local directory but are on the S3
  bucket
* not touch anything else
* and, OH YEAH. It will set mime types via a combination of extension
  lookup and libmagic. Which *neither* of `awscli` or `s3cmd` will do,
  even though it's what you want to do in 99% of the cases, because
  that's what Apache does. Apache is sensible. Let's be sensible.

Beware: written in angry. I had work to do this morning, damn it.

## Dependencies

* python
* python's libmagic (`pip install libmagic`)
* amazon's cli tools (`pip install awscli`)

