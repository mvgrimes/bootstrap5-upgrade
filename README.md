# Upgrade Bootstrap v4 to v5

Tools to help automate the upgrading a project from Bootstrap v4 to v5 and
reactstrap v8 to v9.

## Prerequisites

Other than perl v5.20 or later, the only prerequisite in the `Path::Tiny`
module. This can be installed from CPAN with the builtin `cpan` tool or
`cpanm`. Most perl users recommend using cpanminus these days. Check the
[cpanminus documentation](https://metacpan.org/pod/App::cpanminus) for
installation instructions.

Then install `Path::Tiny`:

    $ cpan install Path::Tiny
    # or (if cpanm is installed)
    $ cpanm Path::Tiny

## Usage

You can simply run `upgrade-bs5` and supply the directors that hold your
html/Markdown/React/etc which uses Bootstrap v4:

    $ ../bs5/upgrade-bs5 components public pages

The tool will modify files in those directories and sub-directories *in place*.
_Your files will be overwritten._ We assume that your files are all stored in,
version control and already committed, so this is the desired action. No
filtering of directories is done (so if `node_modules` is a subdirectory it
will likely break all sorts of things).

Additionally, the tool will output diagnostics that can be consumed by
Vim/Neovim. These can be used to jump to lines where changes may need to be
made by hand. Inside Vim/Neovim use:

    :cex system("../bs5/upgrade-bs5 components public pages") | copen

### Operation

Many classes have simply changed names from v4 to v5. `upgrade-bs5` attempts to
automatically update thse classes. For example:

        no-gutters -> g-0
        custom-check -> form-check
        custom-switch -> form-switch

Other changes that are simply reported (in a Vim/Neovim errorlist compatible
format). For example:

    order-6 -> Bootstrap now only provides .order-1 to .order-5 out of the box.
    media -> Bootstrap dropped the .media component as it can be easily replicated with utilities.

We have attempted to capture all the breaking changes reported by
[Bootstrap](https://getbootstrap.com/docs/5.0/migration/#utilities) and
[reactstrap](https://getbootstrap.com/docs/5.0/migration/#utilities).

## Warning

Make sure you read the Usage section. If this overwrites all of your code/files
because you used it incorrectly or there was a bug it is your responsibility.

*THIS SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.*
