# Lightroom Unofficial Database Table Reference

More information @ [{DPHacks}](https://dphacks.com/how-to-canon-camera-control-api-ccapi/) website - a website for everything camera hack related

This is a work in progress to document Adobe Lightroom's SQLite database structure.

## Overall Structure

All the tables prefixed with 'Ag' hold image/photo information. Ag is the periodic table symbol for Silver. Photographic film is made of silver halide crystals, so this is Adobe's way of referencing your digital files as your original 'negatives'. Keep that in mind when looking through the tables.

## Main Tables

**AgLibraryFile**

Base table listing all the images in the LR catalog. Table has columns with basic information like file name and extension.

**AgLibraryFolder**

Folder structure under the root folder.\
Main references:\
```AgLibraryFile.folder = AgLibraryFolder.id_local```

**AgLibraryKeyword**

List of all the keywords used

**AgLibraryKeywordImage**

Linkage between images and assigned keywords\
Main references:\
```AgLibraryKeywordImage.image =  Adobe_images.id_local```\
```AgLibraryKeywordImage.tag = AgLibraryKeyword.id_local```

**AgHarvestedExifMetadata**

Holds basic EXIF information like reference to Camera Model, Lens, Date, Focal Length, ISO, Aperture, and Shutter Speed\
Main references:\
```AgHarvestedExifMetadata.image = AgLibraryFile.id_local```

**AgHarvestedIptcMetadata**

Holds basic IPTC information like reference to Camera Model, Lens, Date, Focal Length, ISO, Aperture, and Shutter Speed\
Main references:\


## Tables and Descriptions

**Adobe_AdditionalMetadata** - Holds pretty much all the metadata for a single image file. XMP is the important column here. Adobe used to store this information as XML data but decided to store it as binary data in newer versions of LR\
Adobe_faceProperties\
Adobe_imageDevelopBeforeSettings\
**Adobe_imageDevelopSettings** - Settings from sliders applied to the image. Column "text" has a JSON with adjustments applied.\
**Adobe_imageProofSettings** - Basic information about ICC profiles loaded into LR\
Adobe_imageProperties\
**Adobe_images** - Basic information about an image\
Adobe_libraryImageDevelop3DLUTColorTable\
Adobe_libraryImageDevelopHistoryStep\
Adobe_libraryImageDevelopSnapshot\
Adobe_libraryImageFaceProcessHistory\
**Adobe_namedIdentityPlate** - LR Identity plate information\
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
**AgInternedExifCameraModel** - Camera model name\
**AgInternedExifCameraSN** - Camera model serial number\
**AgInternedExifLens** - Lens name\
**AgInternedIptcCity** - IPTC City information. This table also gets populated for photos with GPS coordinates, from the Map module\
**AgInternedIptcCountry** - IPTC Country information. This table also gets populated for photos with GPS coordinates, from the Map module\
**AgInternedIptcCreator** - IPTC Creator information.\
**AgInternedIptcIsoCountryCode** - IPTC Country (ISO Code) information. This table also gets populated for photos with GPS coordinates, from the Map module\
AgInternedIptcJobIdentifier\
**AgInternedIptcLocation** - Stores the image's 'sublocation'. This table also gets populated for photos with GPS coordinates, from the Map module\
**AgInternedIptcState** - IPTC State information. This table also gets populated for photos with GPS coordinates, from the Map module. Not all images get a 'sublocation'\
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
**AgLibraryKeyword** - List of all the keywords used in the catalog\
AgLibraryKeywordCooccurrence\
AgLibraryKeywordFace\
**AgLibraryKeywordImage** - Keywords and all associated images\
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

## Sample SQLite Queries

### Number of Pictures by Camera

```sql
SELECT AgInternedExifCameraModel.value as 'Camera', count(AgHarvestedExifMetadata.id_local) as 'Count'
FROM
	AgHarvestedExifMetadata,
	AgInternedExifCameraModel
WHERE
	AgHarvestedExifMetadata.cameraModelRef = AgInternedExifCameraModel.id_local
GROUP BY
	Camera
ORDER BY
	Count DESC
```

### Number of Pictures by Lens

```sql
SELECT AgInternedExifLens.value as 'Lens', count(AgHarvestedExifMetadata.id_local) as 'Count'
FROM
	AgHarvestedExifMetadata,
	AgInternedExifLens
WHERE
	AgHarvestedExifMetadata.lensRef = AgInternedExifLens.id_local
GROUP BY
	Lens
ORDER BY
	Count DESC
```
