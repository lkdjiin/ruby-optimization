
assignment
----------

``` ruby
def parallel
  a, b = 1, 2
end

def two_lines
  a = 1
  b = 2
end
```

                    user     system      total        real
    parallel    0.140000   0.000000   0.140000 (  0.134804)
    two_lines   0.080000   0.000000   0.080000 (  0.087994)

**75% slower**

symbol
---------

``` ruby
def a
  (1..100).map {|i| i.to_s }
end

def b
  (1..100).map(&:to_s)
end
```

            user     system      total        real
    a   1.980000   0.000000   1.980000 (  1.984782)
    b   1.980000   0.000000   1.980000 (  1.976912)

**equal time**

gsub vs sub
-----------

``` ruby
def a
  'hello world'.gsub(' ', '_')
end

def b
  'hello world'.sub(' ', '_')
end
```

            user     system      total        real
    a   3.620000   0.000000   3.620000 (  3.619890)
    b   2.000000   0.000000   2.000000 (  2.002724)

**81% slower**

gsub vs tr
----------

``` ruby
def a
  'hello world I am here'.gsub(' ', '_')
end

def b
  'hello world I am here'.tr(' ', '_')
end
```

            user     system      total        real
    a   4.830000   0.000000   4.830000 (  4.824694)
    b   0.570000   0.000000   0.570000 (  0.576492)

**847% slower**

control flow
------------

``` ruby
def a
  begin
    unknown
  rescue
    false
  end
end

def b
  if respond_to?(:unknown)
    true
  else
    false
  end
end
```

            user     system      total        real
    a   0.290000   0.000000   0.290000 (  0.289603)
    b   0.020000   0.000000   0.020000 (  0.019376)

**1450% slower**

hash
-------

``` ruby
def a
  hash = { foo: 'foo' }
  hash.merge({ bar: 'bar' })
end

def b
  hash = { foo: 'foo' }
  hash.merge!({ bar: 'bar' })
end

def c
  hash = { foo: 'foo' }
  hash[:bar] = 'bar'
end
```

            user     system      total        real
    a   2.260000   0.000000   2.260000 (  2.259769)
    b   1.150000   0.000000   1.150000 (  1.151173)
    c   1.140000   0.000000   1.140000 (  1.142320)

