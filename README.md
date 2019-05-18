# Lightroom Unofficial Database Table Catalog

This is a work in progress to document Adobe Lightroom's SQLite database structure.

## Overall Structure

All the tables prefixed with 'Ag' hold image/photo information. Ag is the periodic table symbol for Silver. Photographic film is made of silver halide crystals, so this is Adobe's way of referencing your digital files as your original 'negatives'. Keep that in mind when looking through the tables.

## Main Tables

**AgLibraryFile**

Base table listing all the images in the LR catalog. Table has columns with basic information like file name and extension.

**AgLibraryFolder**

Folder structure under the root folder.\
Main reference: ```AgLibraryFile.folder = AgLibraryFolder.id_local```

**AgLibraryKeyword**

List of all the keywords used

**AgLibraryKeywordImage**

Linkage between images and assigned keywords\
Main reference: ```AgLibraryKeywordImage.image =  Adobe_images.id_local``` ```AgLibraryKeywordImage.tag = AgLibraryKeyword.id_local```

**AgHarvestedExifMetadata**

Holds basic EXIF information like reference to Camera Model, Lens, Date, Focal Length, ISO, Aperture, and Shutter Speed\
Main reference: ```AgHarvestedExifMetadata.image = AgLibraryFile.id_local```



## Tables and Descriptions

Adobe_AdditionalMetadata\
Adobe_faceProperties\
Adobe_imageDevelopBeforeSettings\
**Adobe_imageDevelopSettings** - Settings from sliders applied to the image. Column "text" has a JSON with adjustments applied.\
**Adobe_imageProofSettings** - Basic information about ICC profiles loaded into LR\
Adobe_imageProperties\
Adobe_images - Basic information about an image\
Adobe_libraryImageDevelop3DLUTColorTable\
Adobe_libraryImageDevelopHistoryStep\
Adobe_libraryImageDevelopSnapshot\
Adobe_libraryImageFaceProcessHistory\
Adobe_namedIdentityPlate - LR Identity plate information\
Adobe_variables\
Adobe_variablesTable\
AgDNGProxyInfo\
AgDNGProxyInfoUpdater\
AgDeletedOzAlbumAssetIds\
AgDeletedOzAlbumIds\
AgDeletedOzAssetIds\
AgDeletedOzSpaceIds\
AgFolderContent\
AgHarvestedDNGMetadata\
AgHarvestedExifMetadata\
AgHarvestedIptcMetadata\
AgHarvestedMetadataWorklist\
AgInternedExifCameraModel\
AgInternedExifCameraSN\
AgInternedExifLens\
AgInternedIptcCity\
AgInternedIptcCountry\
AgInternedIptcCreator\
AgInternedIptcIsoCountryCode\
AgInternedIptcJobIdentifier\
AgInternedIptcLocation\
AgInternedIptcState\
AgLastCatalogExport\
AgLibraryCollection\
AgLibraryCollectionChangeCounter\
AgLibraryCollectionContent\
AgLibraryCollectionCoverImage\
AgLibraryCollectionImage\
AgLibraryCollectionImageChangeCounter\
AgLibraryCollectionImageOzAlbumAssetIds\
AgLibraryCollectionImageOzSortOrder\
AgLibraryCollectionOzAlbumIds\
AgLibraryCollectionStack\
AgLibraryCollectionStackData\
AgLibraryCollectionStackImage\
AgLibraryCollectionSyncedAlbumData\
AgLibraryCollectionTrackedAssets\
AgLibraryFace\
AgLibraryFaceCluster\
AgLibraryFaceData\
AgLibraryFile\
AgLibraryFileAssetMetadata\
AgLibraryFolder\
AgLibraryFolderFavorite\
AgLibraryFolderLabel\
AgLibraryFolderStack\
AgLibraryFolderStackData\
AgLibraryFolderStackImage\
AgLibraryIPTC\
AgLibraryImageChangeCounter\
AgLibraryImageOzAssetIds\
AgLibraryImageSearchData\
AgLibraryImageSyncedAssetData\
AgLibraryImageXMPUpdater\
AgLibraryImport\
AgLibraryImportImage\
AgLibraryKeyword\
AgLibraryKeywordCooccurrence\
AgLibraryKeywordFace\
AgLibraryKeywordImage\
AgLibraryKeywordPopularity\
AgLibraryKeywordSynonym\
AgLibraryOzCommentIds\
AgLibraryOzFavoriteIds\
AgLibraryOzFeedbackInfo\
AgLibraryPublishedCollection\
AgLibraryPublishedCollectionContent\
AgLibraryPublishedCollectionImage\
AgLibraryRootFolder\
AgLibraryUpdatedImages\
AgMRULists\
AgMetadataSearchIndex\
AgOutputImageAsset\
AgOzSpaceAlbumIds\
AgOzSpaceIds\
AgPendingOzAlbumAssetIds\
AgPendingOzAssetBinaryDownloads\
AgPendingOzAssets\
AgPhotoComment\
AgPhotoProperty\
AgPhotoPropertyArrayElement\
AgPhotoPropertySpec\
AgPublishListenerWorklist\
AgRemotePhoto\
AgSearchablePhotoProperty\
AgSearchablePhotoPropertyArrayElement\
AgSourceColorProfileConstants\
AgSpecialSourceContent\
AgTempImages\
AgUnsupportedOzAssets\
AgVideoInfo\
LrMobileSyncChangeCounter\
MigratedCollectionImages\
MigratedCollections\
MigratedImages\
MigratedInfo\
MigrationSchemaVersion\

## Tables and Fields