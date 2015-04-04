# Dialyzer PLTs for Elixir on Travis CI

The persistent lookup tables in this repository were generated for various
versions of Elixir and OTP releases.

The file format is: `elixir-#{elixir_version}_#{otp_version}`.

## Sample .travis.yml

From my [blog post](http://blog.danielberkompas.com/elixir/2015/04/03/run-dialyzer-on-elixir-on-travis.html):

```yaml
language: elixir
otp_release:
  - 17.4
before_script:
  # Set download location
  - export PLT_FILENAME=elixir-${TRAVIS_ELIXIR_VERSION}_${TRAVIS_OTP_RELEASE}.plt
  - export PLT_LOCATION=/home/travis/$PLT_FILENAME
  # Download PLT from danielberkompas/travis_elixir_plts on Github
  # Store in $PLT_LOCATION
  - wget -O $PLT_LOCATION https://raw.github.com/danielberkompas/travis_elixir_plts/master/$PLT_FILENAME
script:
  - mix test
  - dialyzer --no_check_plt --plt $PLT_LOCATION --no_native _build/test/lib/$YOUR_PROJECT_NAME/ebin
```

Where `_build/test/lib/$YOUR_PROJECT_NAME/ebin` is the location of your compiled
BEAM files.
