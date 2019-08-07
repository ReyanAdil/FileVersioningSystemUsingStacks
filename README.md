# FileVersioningSystemUsingStacks
Industry Demonstration: File Versioning System

You will now see an implementation of stacks. As our professor said in one of the previous videos, one of the applications of stacks is the Undo feature used by word-processing tools. What this feature does is that it uses the ‘file versioning system’ to restore a previous version of a file. So, let’s explore how the file versioning system is implemented using stacks.

Code snippets of some of the important methods used in VersioningService.java:
    /**
     * Returns the current version i.e. the most recent version. (top of the stack)
     *
     * @return
     */
    public Version<T> getCurrentVersion() {
        return this.versionStack.peek();
    }
 
    /**
     * Returns the total number of versions
     * in the hierarchy chain.
     *
     * @return
     */
    public int getNumberOfVersions() {
        return this.versionStack.size();
    }
 
    /**
     * Returns a former version. The `hops` parameter defines how far back we
     * look for this version in the history (version hierarchy)
     *
     * @param hops
     * @return
     */
    public Version<T> getFormerVersion(int hops) {
        this.validateGetVersionRequest(hops);
        // in case we are going back as many versions as are in the stack, the return value will
        // be null, since no version is defined.
        if (hops == this.versionStack.size()) {
            return null;
        }
        return this.versionStack.elementAt((this.versionStack.size() - 1) - hops);
    }
 
    /**
     * Resets the version hierarchy to a previous version. The `hops` denotes the
     * number of versions (counted from the latest/most recent version) we go back
     * in the version history.
     *
     * @param hops
     */
    public void revertToFormerVersion(int hops) {
        this.validateGetVersionRequest(hops);
        // for every hop, we pop a single version off the top of the stack.
        while (hops > 0) {
            this.versionStack.pop();
            hops--;
        }
    }
 
